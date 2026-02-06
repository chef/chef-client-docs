+++
title = "REST resource guide"


[menu]
  [menu.resources]
    title = "REST resource"
    identifier = "resources/custom/rest"
    parent = "resources/custom"
    weight = 50
+++

The REST resource (`rest_resource`) is a base resource class in Chef Infra Client that simplifies the creation of custom resources for managing REST API endpoints. Instead of writing HTTP request handling code from scratch, you can extend this resource to create custom resources that automatically handle API interactions, JSON mapping, and state management.

With the REST resource you can:

- Define resource properties that map directly to API fields
- Use built-in actions to create, update, and delete resources with REST APIs
- Create nested JSON structures using JMESPath expressions

## Create a custom REST resource

To create a custom REST resource:

1. Create a resource class with the `core::rest_resource` partial
1. Configure REST API endpoints
1. Define your resource properties
1. Map properties to JSON fields

## Basic example

This example does the following:

- creates the `ApiUser` resource class with the `"core::rest_resource"` partial
- defines an API document and collection
- defines resource properties
- map properties to JSON API fields
- in a recipe, use the custom resource to manage users

```ruby
class Chef::Resource::ApiUser < Chef::Resource
  use "core::rest_resource"  # Include REST resource functionality

  resource_name :api_user
  provides :api_user

  # Configure the API document and collection
  rest_api_collection "/api/v1/users"
  rest_api_document "/api/v1/users/{username}"

  # Define resource properties
  property :username, String, name_property: true, identity: true
  property :email, String, required: true
  property :active, [true, false], default: true

  # Map properties to JSON fields
  rest_property_map({
    username: "username",
    email: "email",
    active: "active"
  })
end
```

Once defined, you can use the custom resource in recipes:

```ruby
# Create or update a user
api_user "jdoe" do
  email "jdoe@example.com"
  active true
  action :configure
end

# Delete a user
api_user "jdoe" do
  action :delete
end
```

## REST resource components

When you call `use "core::rest_resource"`, your resource gains:

- DSL Methods: `rest_api_collection`, `rest_api_document`, `rest_property_map`, `rest_identity_map`, `rest_post_only_properties`
- Actions: `:configure` (default) and `:delete`
- Action Methods: `rest_get`, `rest_post`, `rest_patch`, `rest_delete`, etc.
- Hooks: `rest_postprocess`, `rest_errorhandler`, `rest_headers` (overrideable)
- Helper Methods: Internal methods for JSON mapping, URL building, and state management

### Methods

The REST resource provides several DSL methods for configuring API interactions. These methods are called within your custom resource class definition.

#### rest_api_collection

Defines the base URL for the resource collection. This URL is used for listing resources and creating new ones.

This method has the following syntax:

```ruby
rest_api_collection "/path/to/collection"
```

- Path must be absolute (start with `/`)
- Used for GET (list all) and POST (create) operations

For example:

```ruby
rest_api_collection "/api/v1/users"
```

#### rest_api_document

Defines the URL pattern for individual resource documents. Supports RFC 6570 URI templates for dynamic URLs.

This method has the following syntax:

```ruby
rest_api_document "/path/to/{resource_id}", first_element_only: false
```

Parameters:

- `path` (String): URL pattern with optional `{template}` placeholders
- `first_element_only` (Boolean): If true, extracts first element from array responses

For example:

- Path-based selection:

  ```ruby
  rest_api_document "/api/v1/users/{username}"
  ```

- Query-based selection:

  ```ruby
  rest_api_document "/api/v1/users?name={username}&org={organization}"
  ```

- Handling array responses:

  ```ruby
  rest_api_document "/api/v1/search?q={name}", first_element_only: true
  ```

#### rest_property_map

Maps resource properties to JSON API fields. Supports both simple mappings and complex nested structures.

This method has the following syntax:

```ruby
rest_property_map <MAPPING>
```

Replace `<MAPPING>` with one of the following:

- An array of 1:1 mappings, for example:

  ```ruby
  rest_property_map [:username, :email, :role]
  # Equivalent to: { username: 'username', email: 'email', role: 'role' }
  ```

- A hash mapping resource properties to JSON fields or JMESPaths. For example:

  ```ruby
  rest_property_map({
    property_name: "json.path.to.field",
    another_property: "nested.field",
    custom_property: :custom_mapping_function
  })
  ```

Mapping types

  1. String values: JMESPath expressions for extracting/setting nested values

     ```ruby
     rest_property_map({
       full_name: "profile.fullName",
       email: "contact.email.primary"
     })
     ```

  2. Symbol values: Custom mapping functions (see Custom Mapping Functions below)

     ```ruby
     rest_property_map({
       tags: :tags_mapping  # Uses tags_from_json and tags_to_json methods
     })
     ```

#### rest_identity_map

Explicitly defines which properties uniquely identify a resource. Usually inferred automatically from the document URL, but can be specified for complex cases.

This method has the following syntax:

```ruby
rest_identity_map(<MAPPING>)
```

Replace `<MAPPING>` with a hash mapping JSON paths to property symbols.
For example:

```ruby
# Single identity property
rest_identity_map({ "username" => :username })

# Composite identity
rest_identity_map({
 "user.name" => :username,
 "organization.id" => :org_id
})
```

#### rest_post_only_properties

Declares properties that should only be sent during resource creation (POST) and excluded from updates (PATCH).

This method has the following synatax:

```ruby
rest_post_only_properties <PROPERTY_OR_ARRAY>
```

Replace `<PROPERTY_OR_ARRAY>` with a single symbol or array of symbols representing property names.
For example:

- Single property:

  ```ruby
  rest_post_only_properties :password
  ```

- Multiple properties:

  ```ruby
  rest_post_only_properties [:password, :initial_role, :creation_token]
  ```

Common use cases:

- Passwords or secrets that can't be updated
- Resource size/capacity that's immutable after creation
- Template or source identifiers used only during initialization

### Actions

The REST resource provides two built-in actions:

#### :configure (default)

: Creates a new resource or updates an existing one. This action is idempotent and will:

  - Check if the resource exists by querying the API
  - If it doesn't exist: Send a POST request to create it
  - If it exists and properties changed: Send a PATCH request to update it
  - If it exists and nothing changed: Take no action

  For example:

  ```ruby
  api_user "john" do
    email "john@example.com"
    role "admin"
    action :configure  # This is the default action
  end
  ```

#### :delete

: Deletes a resource with the REST API. This action is idempotent and will:

  - Check if the resource exists
  - If it exists: Send a DELETE request
  - If it doesn't exist: Take no action

  For example:

  ```ruby
  api_user "john" do
    action :delete
  end
  `

### Property mapping

#### JMESPath Expressions

JMESPath is used to navigate and extract data from JSON structures. The REST resource supports JMESPath for both reading from and writing to APIs.

Basic paths:
```ruby
rest_property_map({
  username: "username",           # Top-level field
  email: "contact.email",         # Nested field
  city: "address.location.city"   # Deeply nested field
})
```

Array projections:
```ruby
rest_property_map({
  member_emails: "members[*].email"  # Extract email from each member
})
```

Complex selections:
```ruby
rest_property_map({
  active_users: "users[?active==`true`].name"  # Filter and extract
})
```

#### Custom Mapping Functions

For complex transformations that JMESPath can't handle, use custom mapping functions by specifying a symbol in the property map.

Requirements:
- Symbol `:my_property` requires two methods:
- `my_property_from_json(resource_data)` - Extract value from API response
- `my_property_to_json(property_value)` - Convert value for API request

Example:

```ruby
class Chef::Resource::ApiProject < Chef::Resource
  use "core::rest_resource"

  resource_name :api_project

  property :tags, Hash, default: {}

  rest_property_map({
    name: "name",
    tags: :tags_mapping  # Uses custom functions
  })

  action_class do
    # Convert API's tag array to hash
    def tags_from_json(resource_data)
      tag_array = resource_data["tags"] || []
      tag_array.to_h { |tag| [tag["key"], tag["value"]] }
    end

    # Convert hash to API's tag array format
    def tags_to_json(tags_hash)
      {
        "tags" => tags_hash.map { |k, v| { "key" => k, "value" => v } }
      }
    end
  end
end
```

## Advanced Features

### Custom Headers and Authentication

Override the `rest_headers` method in your action class to add custom headers like authentication tokens.

```ruby
class Chef::Resource::ApiResource < Chef::Resource
  use "core::rest_resource"

  rest_api_collection "/api/v1/resources"

  action_class do
    def rest_headers
      {
        "Authorization" => "Bearer #{node['api_token']}",
        "X-API-Version" => "2024-01-01",
        "Content-Type" => "application/json"
      }
    end
  end
end
```

### Response Post-Processing

Override the `rest_postprocess` method to transform API responses, handle pagination, or extract embedded data.

```ruby
action_class do
  def rest_postprocess(response)
    # Extract data from paginated response
    if response.data.is_a?(Hash) && response.data["items"]
      response.data = response.data["items"]
    end

    # Add custom logging
    Chef::Log.debug("API response: #{response.data.inspect}")

    response
  end
end
```

### Custom Error Handling

Override the `rest_errorhandler` method to provide user-friendly error messages or handle specific error codes.

```ruby
action_class do
  def rest_errorhandler(error_obj)
    case error_obj.response&.code
    when 404
      Chef::Log.warn("Resource not found - it may have been deleted externally")
      nil
    when 429
      raise "API rate limit exceeded. Please try again later."
    when 401, 403
      raise "Authentication failed. Check your API credentials."
    else
      raise error_obj  # Re-raise for unexpected errors
    end
  end
end
```

### Conditional Property Requirements

Use the `conditionally_require_on_setting` helper to enforce dependencies between properties.

```ruby
action_class do
  def load_current_resource
    super

    # If ssl_enabled is true, require ssl_cert and ssl_key
    conditionally_require_on_setting(:ssl_enabled, [:ssl_cert, :ssl_key])
  end
end
```

## Examples

### Create an REST API to manage users

```ruby
class Chef::Resource::ApiUser < Chef::Resource
  use "core::rest_resource"

  resource_name :api_user
  provides :api_user

  rest_api_collection "/api/v1/users"
  rest_api_document "/api/v1/users/{username}"

  property :username, String, name_property: true, identity: true
  property :email, String, required: true
  property :first_name, String
  property :last_name, String
  property :role, String, equal_to: ["admin", "user", "readonly"], default: "user"
  property :active, [true, false], default: true
  property :password, String, sensitive: true

  rest_property_map({
    username: "username",
    email: "email",
    first_name: "profile.firstName",
    last_name: "profile.lastName",
    role: "permissions.role",
    active: "status.active",
    password: "password"
  })

  # Password can only be set during creation
  rest_post_only_properties :password
end

# Usage in a recipe:
api_user "alice" do
  email "alice@example.com"
  first_name "Alice"
  last_name "Smith"
  role "admin"
  password "initial-password-123"
  action :configure
end
```

### Cloud resource with complex mapping

```ruby
class Chef::Resource::CloudServer < Chef::Resource
  use "core::rest_resource"

  resource_name :cloud_server
  provides :cloud_server

  rest_api_collection "/api/v2/servers"
  rest_api_document "/api/v2/servers/{server_id}"

  property :server_id, String, name_property: true, identity: true
  property :name, String, required: true
  property :size, String, required: true
  property :region, String, required: true
  property :image, String, required: true
  property :tags, Hash, default: {}
  property :ssh_keys, Array, default: []

  rest_property_map({
    server_id: "id",
    name: "name",
    size: "size.slug",
    region: "region.slug",
    image: "image.slug",
    tags: :tags_mapping,
    ssh_keys: "ssh_keys[*].id"
  })

  # Size and image can only be set at creation
  rest_post_only_properties [:size, :image]

  action_class do
    # Convert tag hash to API's array format
    def tags_from_json(resource_data)
      tags = resource_data.dig("tags") || []
      tags.to_h { |t| [t["key"], t["value"]] }
    end

    def tags_to_json(tags_hash)
      {
        "tags" => tags_hash.map { |k, v| { "key" => k, "value" => v } }
      }
    end

    def rest_headers
      {
        "Authorization" => "Bearer #{node['cloud_api_token']}",
        "Content-Type" => "application/json"
      }
    end

    def rest_errorhandler(error_obj)
      case error_obj.response&.code
      when 402
        raise "Insufficient credits to create server"
      when 422
        raise "Invalid server configuration: #{error_obj.message}"
      else
        raise error_obj
      end
    end
  end
end

# Usage:
cloud_server "web-01" do
  name "web-server-01"
  size "s-2vcpu-4gb"
  region "nyc3"
  image "ubuntu-22-04-x64"
  tags({ "environment" => "production", "role" => "web" })
  ssh_keys [12345, 67890]
  action :configure
end
```

### Query-based resource selection

This example demonstrates how to use query parameters to identify a unique resource when the API doesn't support path-based resource selection.

```ruby
class Chef::Resource::DnsRecord < Chef::Resource
  use "core::rest_resource"

  resource_name :dns_record
  provides :dns_record

  rest_api_collection "/api/v1/zones/example.com/records"
  rest_api_document "/api/v1/zones/example.com/records?name={record_name}&type={record_type}"

  property :record_name, String, name_property: true
  property :record_type, String, equal_to: ["A", "AAAA", "CNAME", "MX", "TXT"], default: "A"
  property :value, String, required: true
  property :ttl, Integer, default: 3600

  rest_property_map({
    record_name: "name",
    record_type: "type",
    value: "content",
    ttl: "ttl"
  })

  # Explicitly define composite identity
  rest_identity_map({
    "name" => :record_name,
    "type" => :record_type
  })
end

# Usage:
dns_record "www.example.com" do
  record_type "A"
  value "192.0.2.1"
  ttl 300
  action :configure
end
```

### Handle paginated API responses

This example demonstrates how to handle paginated API responses in a custom REST resource.

```ruby
class Chef::Resource::TeamMember < Chef::Resource
  use "core::rest_resource"

  resource_name :team_member
  provides :team_member

  rest_api_collection "/api/v1/teams/engineering/members"
  rest_api_document "/api/v1/teams/engineering/members/{user_id}"

  property :user_id, String, name_property: true, identity: true
  property :role, String, equal_to: ["member", "maintainer", "owner"]

  rest_property_map({
    user_id: "id",
    role: "role"
  })

  action_class do
    # Handle paginated GET responses
    def rest_postprocess(response)
      # API returns: { "data": [...], "pagination": {...} }
      if response.data.is_a?(Hash) && response.data["data"]
        response.data = response.data["data"]
      end

      response
    end

    # Fetch all pages of results
    def rest_get_all
      all_results = []
      page = 1

      loop do
        response = api_connection.get("#{rest_url_collection}?page=#{page}")
        response = rest_postprocess(response)

        break if response.data.empty?

        all_results.concat(response.data)
        page += 1

        break unless response.data.length >= 100  # Assume 100 per page
      end

      # Return mock response with all results
      response.data = all_results
      response
    end
  end
end
```

## Troubleshooting

### Debugging API requests

Enable debug logging to see API requests and responses:

```ruby
action_class do
  def rest_postprocess(response)
    Chef::Log.debug("API Request: #{rest_url_document}")
    Chef::Log.debug("API Response: #{response.data.inspect}")
    response
  end
end
```

### Common issues

Issue: "No such file" error for identity property

This usually means the identity mapping is incorrect or the document URL template doesn't match the property.

```ruby
# Ensure template variables match property names
rest_api_document "/api/v1/users/{username}"  # Template: username
property :username, String, identity: true     # Property: username
```

Issue: Properties not updating

Check if properties are accidentally marked as post-only:

```ruby
rest_post_only_properties [:password]  # Only password is post-only
# Don't include properties that should be updatable
```

Issue: "Can't resolve property to JSON"

Verify your property map includes all properties you're trying to set:

```ruby
property :email, String
property :role, String

rest_property_map({
  email: "email",
  role: "role"  # Don't forget to map all properties
})
```

## Best practices

1. Use Identity Properties: Always mark identity properties with `identity: true`
2. Handle Errors Gracefully: Override `rest_errorhandler` for better error messages
3. Validate Input: Use Chef's property validation (`:equal_to`, `:regex`, etc.)
4. Document Your Resource: Include `description` and `examples` in your custom resource
5. Test Thoroughly: Write ChefSpec unit tests and Test Kitchen integration tests
6. Secure Credentials: Use data bags, encrypted attributes, or external secrets management
7. Handle Pagination: Override `rest_get_all` if the API uses pagination
8. Version Your API: Include API version in the endpoint URL or headers

## Reference

### Inherited methods

When you extend `RestResource`, you inherit these action_class methods:

- `rest_get_all` - Fetch all resources from the collection
- `rest_get` - Fetch a specific resource
- `rest_post(data)` - Create a new resource
- `rest_patch(data)` - Update an existing resource
- `rest_put(data)` - Replace an existing resource
- `rest_delete` - Delete a resource

### Overrideable methods

- `rest_postprocess(response)` - Transform API responses
- `rest_errorhandler(error_obj)` - Handle API errors
- `rest_headers` - Add custom headers to requests

### Helper methods

- `resource_exists?` - Check if resource exists in API
- `property_to_json(property, mapping)` - Convert property to JSON
- `json_to_property(mapping, property, data)` - Extract value from JSON
- `conditionally_require_on_setting(property, dependencies)` - Enforce property dependencies

## Additional resources

- [Chef Custom Resources Documentation](https://docs.chef.io/custom_resources/)
- [JMESPath Tutorial](https://jmespath.org/tutorial.html)
- [RFC 6570 URI Template Specification](https://tools.ietf.org/html/rfc6570)
- [REST API Design Best Practices](https://restfulapi.net/)

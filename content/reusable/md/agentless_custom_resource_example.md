
The following custom resource example runs in Agentless Mode and updates the content of a file defined by the `path` property.

```ruby
# Create a new resource that's available in Target Mode
provides :file_update, target_mode: true

property :path, String, name_property: true
property :content, String, default: ""

default_action :update

load_current_value do |new_resource|
  # Prefix any IO calls with ::TargetIO to use the IO abstraction
  if ::TargetIO::File.exist?(new_resource.path)
    content ::TargetIO::IO.read(new_resource.path)
  end
end

action :update do
  converge_if_changed :content do
    TargetIO.write(new_resource.path, new_resource.content)
    # You can also use shell_out() here without any prefix
  end
end
```

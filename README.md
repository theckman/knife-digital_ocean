# Knife::DigitalOcean

This is a plugin for [Chef's](http://www.opscode.com/chef/) [knife](http://wiki.opscode.com/display/chef/Knife) tool. It allows you to bootstrap virtual machines with [DigitalOcean.com](https://www.digitalocean.com/) including the initial bootstrapping of chef on that system.
You can also skip the chef bootstrapping if you prefer using [knife-solo](https://github.com/matschaffer/knife-solo) or some other solutions.
## Installation
    $ # install chef
    $ gem install knife-digital_ocean

## Overview

This plugin provides the following sub-commands:

* knife digital_ocean droplet create (options)   
  **Creates a virtual machine with or without bootstrapping chef-client**

* knife digital_ocean droplet destroy (options)  
  **Destroys the virtual machine and its data**

* knife digital_ocean droplet list (options)     
  **Lists currently running virtual machines**

* knife digital_ocean image list (options)       
  **Lists available images (snapshots, backups, OS-images)**

* knife digital_ocean region list (options)      
  **Lists the server regions/locations/data-center**

* knife digital_ocean size list (options)        
  **Lists the available server sizes**

* knife digital_ocean sshkey list                
  **Lists name + id of the uploaded known ssh keys**

## Configuration

The best way is to put your API-credentials of DigitalOcean in your knife.rb file of choice:

```ruby
knife[:digital_ocean_client_id] = 'XXXXXXXXXXXX'
knife[:digital_ocean_api_key]   = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY'
```

## Usage

### Create a Droplet

#### With bootstrapping in an chef-server environment:

__Example__

```bash
knife digital_ocean droplet create --server-name awesome-vm1.chef.io \
                                   --image 25306 \
                                   --location 2 \
                                   --size 66 \
                                   --ssh-keys 1234,4567 \
                                   --bootstrap \
                                   --run-list "role[base],role[webserver]"
```

__Syntax__
```bash
knife digital_ocean droplet create --server-name <FQDN> \
                                   --image <IMAGE ID> \
                                   --location <REGION ID> \
                                   --size <SIZE ID> \
                                   --ssh-keys <SSH KEY-ID(s), comma-separated> \
                                   --bootstrap \
                                   --run-list "<RUNLIST>"
```

__Short Syntax__
```bash
knife digital_ocean droplet create --N <FQDN> \
                                   --I <IMAGE ID> \
                                   --L <REGION ID> \
                                   --S <SIZE ID> \
                                   --K <SSH KEY-ID(s), comma-separated> \
                                   --B \
                                   --r "<RUNLIST>"
```


#### With knife-solo, your custom external bootstrapping script or without chef at all

This will just create a droplet and returns its IP-address no other actions are done. You can now run your custom solution e.g. ```knife solo bootstrap <IP> ``` 
__Example__

```bash
knife digital_ocean droplet create --server-name awesome-vm1.chef.io \
                                   --image 25306 \
                                   --location 2 \
                                   --size 66 \
                                   --ssh-keys 1234,4567
```


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

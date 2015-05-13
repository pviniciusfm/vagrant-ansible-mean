Development Environment MEAN and Vagrant
=====================================

This configuration will install the latest versions of MongoDB, Nginx, Node.js, Express, Yeoman, and the Yeoman Angular.js generator. Ruby and the compass gem are installed for the yo build process.

All running on the Ubuntu 14.04.2LTS (Trusty Tahr)

Installation
------------
1. Install [Vagrant 1.7.2](http://downloads.vagrantup.com/)
2. Install [VirtualBox 4.6](https://www.virtualbox.org/wiki/Downloads)
3. Install [Ansible](http://www.ansibleworks.com/docs/intro_installation.html)

Running
-------
Running and provisioning can be handled nicely:

```
vagrant up
```

You can SSH into the provisioned vm like so:

```
vagrant ssh
```

And stop it:

```
vagrant halt
```

You have a development enviroment with the latest and greatest Node.js, MongoDB, and Yeoman.

Note: part of the provisioning process ensures that Mongo is already running on it's default port.

Ansible
-------
Ansible is configured to run for the vagrant host and you can see the specified private IP in `provisioning/hosts`. 

If for some reason you want to use a different IP, be aware that you will need to update the `Vagrantfile` as well as `provisioning/hosts`.

```ruby
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.111.222"
end
```

Ansible installs the following packages:
* git
* ruby
* nodejs
* mongodb
* yeoman
* generator-angular for yeoman
* express
* nginx

The mongodb and nginx services are started after provisioning takes place.

Synced Folders
--------------
By default this repo disables directory syncing. If you wish to have this environment checked in as part of the dev process you can create your source directory in the top level of the project and uncomment this line in the `Vagrantfile`:

```ruby
# config.vm.synced_folder "src/", "/home/vagrant/path/to/your/project"
```

This will sync your source folders over SSH so you can develop on your host machine.

Ansible Variables
-----------------
The file `provisioning/group_vars/all` contains configurations for your install. This will allow you to configure project directories and things like nginx hostname and the port node js will run on.

VM Configuration
----------------
For more on VM configuration options, check out the docs at [Vagrant](http://docs.vagrantup.com/v2/virtualbox/configuration.html)

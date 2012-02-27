!SLIDE
## Installation and Usage ##

    @@@ sh
    gem install vagrant
    vagrant box add lucid32 http://.../lucid32.box
    vagrant init lucid32

!SLIDE
## ssh ##
    @@@ sh
    vagrant up
    vagrant ssh
    cd /vagrant
    sudo apt-get install ...

!SLIDE
## Config File ##

    $ ls
    Vagrantfile

!SLIDE
## Setup ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.box = "lucid32"
      config.vm.box_url = "http://.../lucid32.box"
    end

!SLIDE
## Customize box ##
    @@@ruby
    Vagrant::Config.run do |config|
      config.vm.provision :shell, 
        :inline => "echo foo > /vagrant/test"
    end

!SLIDE
## Port Forwarding ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.forward_port 3000, 3000
      config.vm.forward_port 27017, 27017
      config.vm.forward_port 28017, 28017
      config.vm.forward_port 6379, 6379  
      config.vm.forward_port 11211, 11211
    end

!SLIDE
## Share Folder ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.share_folder "v-root", "/vagrant", "."
    end

!SLIDE

## Control Multiple VMs ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.define :web do |web_config|
        web_config.vm.network "33.33.33.10"
        web_config.vm.box = "web"
      end      

      config.vm.define :db do |db_config|
        db_config.vm.network "33.33.33.11"
        db_config.vm.box = "mongo"
      end
    end

!SLIDE
## Package your own box ##

    $ vagrant package  
    package.box

!SLIDE full-screen-image image-only
![](vagrantboxes.png)

!SLIDE full-screen-image
![](vagrantbox2.png)
## Self Hosting Box Server  ##

!SLIDE
## Workflow (1) ##

    @@@ sh
    git add Vagrantfile
    git commit -m "add vagrant file"
    git push origin master

!SLIDE
## Workflow (2) ##

    @@@ sh
    git pull
    vagrant up
    vagrant ssh
    cd /vagrant
    rails s

!SLIDE
## Pause ##

    @@@ sh
    vagrant suspend
    vagrant resume
    
!SLIDE
## Complete ##

    @@@ sh
    vagrant halt
    vagrant destroy
    
!SLIDE
## Restart ##

    @@@ sh
    vagrant up
!SLIDE 
# 用 Vagrant 快速建立開發環境 #

Francis Chong

!SLIDE
# 網路軟件 #

!SLIDE

# 複雜的開發環境 #

!SLIDE

# 問題 #

!SLIDE

## 1. 設定新電腦

!SLIDE

## 2. 長期運行不同的全套資料庫和服務

!SLIDE

## 3. 不同版本的服務

!SLIDE

![](http://www.pittsburghurbanmedia.com/clientfiles/image/mission_impossible.jpg)

!SLIDE

# 解決方法？

!SLIDE 

# Virtualization 

!SLIDE

# Vagrant

!SLIDE

# 甚麼是 vagrant ？

!SLIDE

## 一套建立和管理虛擬機的軟件

!SLIDE

## 安裝和執行

    gem install vagrant
    vagrant box add lucid32 http://files.vagrantup.com/lucid32.box
    vagrant init lucid32
    vagrant up

!SLIDE
## Vagrantfile

    > ls
    Vagrantfile

!SLIDE
## Basic Config ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.box = "lucid32"
      config.vm.box_url = "http://files.vagrantup.com/lucid32.box"
    end

!SLIDE
## Box customization ##
    @@@ruby
    Vagrant::Config.run do |config|
      config.vm.provision :shell, :inline => "echo foo > /vagrant/test"
    end

!SLIDE
## Port Forwarding ##

    @@@ ruby
    Vagrant::Config.run do |config|
      config.vm.forward_port "rails", 3000, 3000
      config.vm.forward_port "mongo", 27017, 27017
      config.vm.forward_port "mongo-http", 28017, 28017
      config.vm.forward_port "redis", 6379, 6379  
      config.vm.forward_port "memcached", 11211, 11211
    end

!SLIDE
## Share Folder ##

    @@@ ruby
    Vagrant::Config.run do |config|
      # Default
      config.vm.share_folder "v-root", "/vagrant", "."
      
      # Custom
      config.vm.share_folder "v-home", "/home/vagrant/documents", "~/Documents", :nfs => true
    end

!SLIDE

## Multiple VMs

    @@@ ruby
    Vagrant::Config.run do |config|
      # Default
      config.vm.define :app do |app|
        app.vm.network "33.33.33.10"
        app.vm.box = "web"
      end
      
      config.vm.define :db do |db|
        app.vm.network "33.33.33.11"
        db.vm.box = "mongo"
      end
    end

!SLIDE
## 登入 ssh ##

    vagrant ssh
    cd /vagrant
    sudo apt-get install ...

!SLIDE
## 包裝自己的 Vagrant Box ##

    > vagrant package  
    => package.box

!SLIDE

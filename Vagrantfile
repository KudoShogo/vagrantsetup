# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :webdb do |webdb|
    webdb.vm.box = "bento/centos-7.3"
    webdb.vm.network "forwarded_port", guest: 3306,  host: 12000, host_ip: "127.0.0.1" # mysql
    webdb.vm.network "forwarded_port", guest: 80,    host: 12002, host_ip: "127.0.0.1" # http
    webdb.vm.network "forwarded_port", guest: 11211, host: 12003, host_ip: "127.0.0.1" # memcached
    webdb.vm.network "private_network", ip: "192.168.30.50"
    webdb.vm.synced_folder "./ansible", "/home/vagrant/ansible", :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=775', 'fmode=775']
    webdb.vm.synced_folder "./pj/pppp", "/var/www/pppp", :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=775', 'fmode=775']
    webdb.vm.synced_folder "./pj/laravel", "/var/www/html", :owner=> 'vagrant', :group=>'vagrant', :mount_options => ['dmode=777', 'fmode=777']
    webdb.vm.provider :virtualbox do |vbox|
      vbox.name = "valeur-laravel"
      vbox.memory = "2048"
    end
    webdb.ssh.insert_key = false
    webdb.vm.provision "shell", run: "always", inline: <<-SHELL
      sudo mv -f /etc/resolv.conf /etc/resolv.conf.org
      sudo sed -e "s/10.0.2.3/8.8.8.8/" /etc/resolv.conf.org >> /etc/resolv.conf
    SHELL
    webdb.vm.provision "shell", inline: <<-SHELL
      sudo yum -y install ansible;
      cd ansible;
      ansible-playbook -i hosts-Valeur -c local site-Valeur.yml -t webdb
    SHELL
  end

end

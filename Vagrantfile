 Vagrant.configure("2") do |config|
   config.hostmanager.enabled = true
   config.vm.box = "geerlingguy/centos7"
   config.vm.synced_folder "vpro_app", "/root"
   config.vm.network 'public_network'
   config.vm.provision :shell, inline: <<-SHELL
   sudo yum update 
   sudo yum install epel-release -y
   sudo yum update 
   sudo yum install python2.7 -y
   sudo yum install python-pip -y
   sudo yum install fabric -y  
   SHELL
############################################ INSTALLING CI SERVER ############################################################################

   config.vm.define "ci" do |build|
     build.vm.hostname = 'build.com'
     build.vm.network "private_network", ip: "192.168.10.20"
     build.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
     fab ci_c
   SHELL
  end

############################################ INSTALLING APP SERVER ###############################################################################

   config.vm.define "app" do |app|
     app.vm.hostname = 'app.com'
     app.vm.network "private_network", ip: "192.168.10.21"
     app.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
      fab app_c 
   SHELL
  end

############################################ INSTALLING DB SERVER ###############################################################################
   config.vm.define "db" do |db|
     db.vm.hostname = 'db.com'
     db.vm.network "private_network", ip: "192.168.10.22"
     db.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
     fab db_c
   SHELL
  end

############################################ INSTALLING LB SERVER ###############################################################################
   config.vm.define "lb" do |lb|
     lb.vm.hostname = 'lb.com'
     lb.vm.network "private_network", ip: "192.168.10.23"
     lb.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
     fab lb_c
   SHELL
  end

############################################ INSTALLING MEMCACHE SERVER ###############################################################################
   config.vm.define "mem" do |mem|
     mem.vm.hostname = 'mem.com'
     mem.vm.network "private_network", ip: "192.168.10.24"
     mem.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
     fab memcache_c
   SHELL
  end

############################################ INSTALLING RABBITMQ SERVER ###############################################################################
   config.vm.define "rmq" do |rmq|
     rmq.vm.hostname = 'rmq.com'
     rmq.vm.network "private_network", ip: "192.168.10.25"
     rmq.vm.provision :shell, inline: <<-SHELL
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes'/ /etc/ssh/sshd_config
     sudo systemctl restart sshd
     cd /root
     fab rabbitmq_c
   SHELL
  end

end

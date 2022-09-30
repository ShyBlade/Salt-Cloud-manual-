# Setting up Salt-Cloud with  vagrant

the vagrant driver is a new experimental driver for spinning ip a vagrantbox virtual machine and installing salt on it. 

## what is vagrant ? 

Vagrant is an open-source software product for building and maintaining portable virtual software development environments; e.g., for VirtualBox, KVM, Hyper-V, Docker containers, VMware, and AWS. It tries to simplify the software configuration management of virtualization in order to increase development productivity


follow this instruction to install vagrtant on ubuntu https://linuxhint.com/install-vagrant-ubuntu/ 
## Dependencies 

The machine which will host the VagrantBox must be an already existing minion of the cloud server's Salt master. It must have Vagrant installed, and a Vagrant-compatible virtual machine engine, such as VirtualBox. (Note: The Vagrant driver does not depend on the salt-cloud VirtualBox driver in any way.)


[Caution: The version of Vagrant packaged for apt install in Ubuntu 16.04 will not connect a bridged network adapter correctly. Use a version downloaded directly from the web site.]
Include the Vagrant guest editions plugin: vagrant plugin install vagrant-vbguest.

## configuration 

Configuration of the client virtual machine (using VirtualBox, VMware, etc) will be done by Vagrant as specified in the Vagrantfile on the host machine.

Salt-cloud will push the commands to install and provision a salt minion on the virtual machine, so you need not (perhaps should not) provision salt in your Vagrantfile, in most cases.






put the following code in the file /etc/salt/cloud.providers or any file in
the /etc/salt/cloud.providers.d/ directory. on your salt minion 


              # Note: This example is for /etc/salt/cloud.providers file or any file in
              # the /etc/salt/cloud.providers.d/ directory.

              my-vagrant-config:
              minion:
              master: 111.222.333.444
             provider: vagrant
             
             

Because the Vagrant driver needs a place to store the mapping between the node name you use for Salt commands and the Vagrantfile which controls the VM, you must configure your salt minion as a Salt smb server.
The Salt sdb is not configured by default. The following example shows a simple installation.

## configuration for salt smb server
put the following example in etc/salt/minion.d/vagrant_sdb.conf:

             # file /etc/salt/minion.d/vagrant_sdb.conf on host computer "my_laptop"
             #  -- this sdb database is required by the Vagrant module --
             vagrant_sdb_data:  # The sdb database must have this name.
             driver: sqlite3  # Let's use SQLite to store the data ...
             database: /var/cache/salt/vagrant.sqlite  # ... in this file ...
             table: sdb  # ... using this table name.
             create_table: True  # if not present


then restart your minion 
        
        sudo systemctl restart salt-minion 
        
 
 put the following within your vagrant file:
 
 
               
               # -*- mode: ruby -*-
                # file /home/my_username/Vagrantfile on host computer "my_laptop"
                BEVY = "bevy1"
                 DOMAIN = BEVY + ".test"  # .test is an ICANN reserved non-public TLD

                  # must supply a list of names to avoid Vagrant asking for interactive input
                  def get_good_ifc()   # try to find a working Ubuntu network adapter name
                  addr_infos = Socket.getifaddrs
                   addr_infos.each do |info|
                    a = info.addr
                     if a and a.ip? and not a.ip_address.start_with?("127.")
                      return info.name
                      end
                      end
                      return "eth0"  # fall back to an old reliable name
                      end

                     Vagrant.configure(2) do |config|
                     config.ssh.forward_agent = true  # so you can use git ssh://...

                     # add a bridged network interface. (try to detect name, then guess MacOS names, too)
                    interface_guesses = [get_good_ifc(), 'en0: Ethernet', 'en1: Wi-Fi (AirPort)']
                   config.vm.network "public_network", bridge: interface_guesses
                   if ARGV[0] == "up"
                  puts "Trying bridge network using interfaces: #{interface_guesses}"
                    end
                 config.vm.provision "shell", inline: "ip address", run: "always"  # make user feel good

                   # . . . . . . . . . . . . Define machine QUAIL1 . . . . . . . . . . . . . .
                   config.vm.define "quail1", primary: true do |quail_config|
                   quail_config.vm.box = "boxesio/xenial64-standard"  # a public VMware & Virtualbox box
                   quail_config.vm.hostname = "quail1." + DOMAIN  # supply a name in our bevy
                   quail_config.vm.provider "virtualbox" do |v|
                   v.memory = 1024       # limit memory for the virtual box
                    v.cpus = 1
                      v.linked_clone = true # make a soft copy of the base Vagrant box
                      v.customize ["modifyvm", :id, "--natnet1", "192.168.128.0/24"]  # do not use 10.x network for NAT
                      end
                      end
                      end




put the follwing example in  file /etc/salt/cloud.profiles.d/my_vagrant_profiles.conf on your salt-cloud master:

                          # file /etc/salt/cloud.profiles.d/my_vagrant_profiles.conf on bevymaster
                        q1:
                          host: my_laptop  # the Salt id of your virtual machine host
                         machine: quail1   # a machine name in the Vagrantfile (if not primary)
                         vagrant_runas: my_username  # owner of Vagrant box files on "my_laptop"
                         cwd: '/home/my_username' # the path (on "my_laptop") of the Vagrantfile
                         provider: my_vagrant_provider  # name of entry in provider.conf file
                         target_network: '10.0.0.0/8'  # VM external address will be somewhere here
                         
                         
                         
                         
                         
                         
                         
                         
  put the following example in  /etc/salt/cloud.providers.d/vagrant_provider.conf on your salt-cloud master 
  
  
  
  
                          # file /etc/salt/cloud.providers.d/vagrant_provider.conf on bevymaster
                          my_vagrant_provider:
                          driver: vagrant
                          minion:
                          master: 10.124.30.7  # the hard address of the master
      


## profiles configuration 
Vagrant requires a profile to be configured for each machine that needs Salt installed. The initial profile can be set up at /etc/salt/cloud.profiles or in the /etc/salt/cloud.profiles.d/ directory.


put the following example in  /etc/salt/cloud.profiles.d/vagrant.conf
           
           #/etc/salt/cloud.profiles.d/vagrant.conf

            vagrant-machine:
           host: my-vhost  # the Salt id of the virtual machine's host computer.
           provider: my-vagrant-config
           cwd: /srv/machines  # the path to your Vagrantfile.
          vagrant_runas: my-username  # the username who defined the Vagrantbox on the host
           # vagrant_up_timeout: 300 # (seconds) timeout for cmd.run of the "vagrant up" command
           # vagrant_provider: '' # option for "vagrant up" like: "--provider vmware_fusion"
           # ssh_host: None  # "None" means try to find the routable IP address from "ifconfig"
           # ssh_username: '' # also required when ssh_host is used.
           # target_network: None  # Expected CIDR address range of your bridged network
           # force_minion_config: false  # Set "true" to re-purpose an existing VM
           
           
           
           
           

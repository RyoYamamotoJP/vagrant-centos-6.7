# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = 'bento/centos-6.7'
  config.vm.box += '-i386' if ENV['PROCESSOR_ARCHITECTURE'] == 'x86'
  config.vm.provision 'shell', inline: <<-SHELL
    sudo yum update -y -x kernel*
    sudo cp -f /usr/share/zoneinfo/Japan /etc/localtime
    sudo cp -f /dev/null /etc/securetty
    sudo sed -i -e 's/^#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
    sudo service sshd reload
    for service in auditd blk-availability kdump lvm2-monitor mdmonitor netfs nfslock postfix rpcgssd rpcbind udev-post
    do
      sudo service $service stop
      sudo chkconfig $service off
    done
  SHELL
end

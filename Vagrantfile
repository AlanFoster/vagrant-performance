# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.define "DC01" do |vm_config|
        vm_config.vm.box = "StefanScherer/windows_2016"
        vm_config.vm.box_version = "2019.02.14"
        vm_config.vm.hostname = "DC01"

        # Communication configuration
        vm_config.winrm.retry_limit = 60
        vm_config.winrm.retry_delay = 10

        # Use WinRM transport and force plaintext/basic auth - which stops digest initialization errors appearing
        # The documentation has the caveat: Credentials will be transferred in plain text - which is fine for a test lab
        vm_config.winrm.transport = "plaintext"
        vm_config.winrm.basic_auth_only = true

        # IP Accessible from the host machine
        vm_config.vm.network "private_network", ip: '10.10.10.5'

        vm_config.vm.provision "shell", path: "scripts/windows/dc01.ps1"
        vm_config.vm.provision "shell", reboot: true
    end

    config.vm.provider "vmware_desktop" do |v|
        v.gui = true
        v.linked_clone = false
        v.vmx["memsize"] = "4096"
        v.vmx["numvcpus"] = "2"
    end

    config.vm.provider "virtualbox" do |virtualbox|
        # Display the VirtualBox GUI when booting the machine
        virtualbox.gui = true

        # By default Vagrant will check for the VirtualBox Guest Additions when starting a machine; skip it
        # https://github.com/hashicorp/vagrant/blob/2a22359380738ebc3eed2e4a76c6da966ffed19b/website/content/docs/providers/virtualbox/configuration.mdx#checking-for-guest-additions
        virtualbox.check_guest_additions = false

        # Customize memory and CPUs for faster boot/provisioning time
        virtualbox.customize [
            "modifyvm", :id,
            "--memory", "4096",
            "--cpus", "2",
            "--ioapic", "on",
            '--clipboard-mode', 'bidirectional',
            '--draganddrop', 'bidirectional'
        ]
    end
end

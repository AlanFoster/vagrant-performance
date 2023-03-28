## Vagrant Performance

Standalone Vagrantfile plus powershell script that creates an Active Directory controller for testing the performance of Vagrant.

### Steps

Either git clone this repo or create the files in this repository manually:

```
git clone https://github.com/AlanFoster/vagrant-performance.git
```

Then run `vagrant up` to create the VM. Note that the first build will be slow as it downloads the base image first.
Inbetween attempts, run `vagrant destroy` to remove the created VM

Measuring Window's performance:

```powershell
Measure-Command { vagrant up | Out-Default }

# Destroy the VM for running again
vagrant destroy
```

Unix:

```bash
time vagrant up

# Destroy the VM for running again
vagrant destroy
```

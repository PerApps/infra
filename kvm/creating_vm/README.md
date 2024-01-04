# Creating Virtual Machines
In order to create virtual machines, you can use the `virt-install` command along with the following mandatory arguments:
* --name: Specifies the name of the new machine.
* --memory: Defines the amount of allocated memory.
* --vcpus: Determines the number of allocated virtual CPUs.
* --disk (path, size, format): Sets the type and size of the allocated storage.
* --cdrom or --location: Specifies the type and location of the OS installation source.
* --os-variant or --os-type: Used to define the OS variant or type during VM creation.
* --cloud-init: Passes cloud-init metadata to the VM (e.g., --cloud-init meta-data=VMs/meta-data,user-data=VMs/user-data).
    * clouduser-ssh-key: Inject a public key into the guest to provide SSH access to the default cloud-init user account.
    * meta-data: Add a cloud-init meta-data file directly to the ISO.
    * user-data: Add a cloud-init user-data file directly to the ISO.
    * root-password-generate: Generate a new root password for the VM.
    * disable: Disable cloud-init in the VM for subsequent boots.
    * network-config: Add a cloud-init network-config file directly to the ISO.
* --noautoconsole: Don't automatically try to connect to the guest console.
* --initrd-inject: Inject file in VM, e.g., with kickstart (--initrd-inject kickstart.cfg --extra-args="inst.ks=file:/kickstart.cfg").
* --extra-args: Additional kernel command line arguments, e.g., (--graphics none --extra-args='console=ttyS0').
* --graphics: Specifies the graphical display configuration, if none it uses a serial console connection without graphical access.
* --autostart: Start the VM when the host server comes up.
* --import: Skip the OS installation process, and build a guest around an existing disk image.
* --network option allows you to connect the guest to the host network. It has various sub-options:
    * network: Allows you to connect to a virtual network in the host. The syntax is --network network=NAME, where NAME is the name of the virtual network.
    * mac.address: Allows you to set a fixed MAC address for the guest. The syntax is --network mac=MAC_ADDRESS, where MAC_ADDRESS is the desired static MAC address that you want to assign to the guest.

Refer to the [official archlinx documentation](https://man.archlinux.org/man/virt-install.1) for more detailed information.

## List of OS Variants
To retrieve a list of OS variants, use the command `sudo virt-install --os-variant=list`.

## Example of Meta-Data File
The meta-data file used in cloud-init allows you to specify configuration information for your virtual machine.
Here is a breakdown of what you can include:
* instance-id: Set this to the name of the new machine. This should match the `--name `argument used in the `virt-install` command.
* local-hostname: This sets the hostname of the VM.

Here's an example of what a meta-data file might look like:
```yaml
instance-id: k8s-worker-guest
local-hostname: k8s-worker-vm
```

In this example, the VM is assigned the name 'k8s-worker-guest' and the hostname 'k8s-worker-vm'.

Use `---cloud-init meta-data=<meta date file>` arguments whis `virt-install`.

## Example of Network Configuration
Here's an example of a network configuration in a YAML file:
```yaml
network:
    version: 2
    ethernets:
        interface0:
            match:
                macaddress: "<your mac address>"
            dhcp4: false
            dhcp6: false
            addresses:
                - 10.0.0.2/12
            gateway4: 10.0.0.1
            set-name: interface0
            nameservers:
                addresses: [10.0.0.1]
```

This configuration sets up a static IP address, `nameservers addresses` is the dns.

Use `--cloud-init network-config=<network configuration file> --network mac.address="<your mac address>"` arguments whis `virt-install`.
Remember to replace `<your mac address>` with the actual Mac address you want to assign to the interface
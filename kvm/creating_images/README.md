# Creating EL9/CentOS Stream 9 Images
To create an EL9/CentOS Stream 9 image for KVM, follow these steps:

1. **Add Disk**: Use the following command to create a new disk image:
```bash
qemu-img create -f qcow2 centos-stream9.qcow2 5G
```
2. **Get ISO**: Download the CentOS Stream 9 ISO file from the official [CentOS website](https://www.centos.org/download/).

3. **Run Installation**: Use the command below to execute the installation process. This command uses `virt-install` with the previously created disk image and the downloaded ISO file. It also includes the use of a kickstart file (in `el9/kickstart.cfg`) for automatizing the installation process. Be sure to replace `CentOS-Stream-9-x86_64-dvd1.iso` with the path where you have saved the downloaded ISO file.
```bash
virt-install \        
--name centos \
--memory 1024 \
--vcpus 2 \
--disk centos-stream9.qcow2 \
--os-variant centos-stream9 \
--initrd-inject kickstart.cfg \
--extra-args "inst.ks=file:/kickstart.cfg console=ttyS0" \
--graphics none \
--location CentOS-Stream-9-x86_64-dvd1.iso
```

4. Clean Up: After the installation is complete, use virt-sysprep to clean up the system.
```bash
virt-sysprep -d centos
```

5. Undefine the libvirt domain: The defined domain can be undefined using the virsh command.
```bash
virt-sysprep -d centos
```

## Login Workflow
To access the virtual machine through SSH using this image, you need to follow these steps:

1. Use the `--cloud-init clouduser-ssh-key=<your-public-ssh-key>` command arg in virt-install. Replace `<your-public-ssh-key>` with your own public key.

2. After the VM starts, log in using the username cloud-user.
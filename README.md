# ubuntu-libvirt-kvm-doc

## Installation
```bash
sudo apt-get install qemu-kvm libvirt-bin virtinst virt-viewer virt-top
```

## Create a empty disk image
```bash
sudo fallocate -l 8192M /var/lib/libvirt/images/ubuntu-16.04.img
```


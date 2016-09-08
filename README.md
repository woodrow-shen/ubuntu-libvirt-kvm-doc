# ubuntu-libvirt-kvm-doc

## Installation
```bash
sudo apt-get install qemu-kvm libvirt-bin virtinst virt-viewer virt-top
```

## Create a empty disk image
```bash
sudo fallocate -l 16G /var/lib/libvirt/images/ubuntu-16.04.img
```

## Create a VM using virt-install
```bash
sudo virt-install -n xenial -r 1024 \
    --disk path=/var/lib/libvirt/images/ubuntu-16.04.img,bus=virtio,size=4 \
    -c xenial-desktop-amd64.iso \
    --network network=default,model=virtio \
    --graphics vnc,listen=0.0.0.0 \
    --vcpus 4 \ 
    --noautoconsole -v
```

## VM viewer
```bash
virt-viewer -c qemu:///system xenial
```

## VM management
```bash
virsh -c qemu:///system list
virsh -c qemu:///system start <vm-name>
virsh -c qemu:///system shutdown <vm-name>
virsh -c qemu:///system reboot <vm-name>
virsh -c qemu:///system save <vm-name> <vm-save-name>.state
virsh -c qemu:///system restore <vm-name> <vm-save-name>.state
virsh -c qemu:///system destroy <vm-name>

virsh list
virsh start <vm-name>
virsh shutdown <vm-name>
virsh reboot <vm-name>
virsh save <vm-name> <vm-save-name>.state
virsh restore <vm-name> <vm-save-name>.state
virsh destroy <vm-name>
virsh undefine <vm-name>
```

## Create a VM using libvirt XML
### Dump XML from existed domain
```bash
virsh dumpxml <vm-name>
```

### Create a VM
```bash
virsh define <vm-name>.xml
```

### Create & Run a VM
```bash
virsh create <vm-name>.xml
```

### Edit VMs Configs
```bash
virsh edit <vm-name>
```

### Delete VMs Configs
```bash
virsh undefine <vm-name>
```

## Control guest CPU & NUMA with kvm/xen
### Querying host CPU / NUMA topology
```bash
virsh nodeinfo
virsh capabilities
```

### Check free memory for NUMA node
```bash
virsh freecell <numa-id>
```

### Automatic placement using virt-install
```bash
virt-install --cpuset=CPUSET
```

### Dump domain vcpu information
```bash
virsh vcpuinfo <vm-name>
```

### Control domain vcpu affinity
```bash
virsh vcpupin <vcpu-id> <cpu-id>
```

## References
https://www.berrange.com/posts/2010/02/12/controlling-guest-cpu-numa-affinity-in-libvirt-with-qemu-kvm-xen/
https://help.ubuntu.com/lts/serverguide/libvirt.html

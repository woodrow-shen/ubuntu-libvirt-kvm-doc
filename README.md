# ubuntu-libvirt-kvm-doc

## Installation
```bash
sudo apt-get install qemu-kvm libvirt-bin virtinst virt-viewer virt-top
```

## Create a empty disk image
```bash
sudo fallocate -l 8192M /var/lib/libvirt/images/ubuntu-16.04.img
```

## Create a VM using virt-install
```bash
sudo virt-install
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

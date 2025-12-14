VFIO GPU Binding (Fedora – Laptop)

This section binds the dedicated GPU to VFIO at boot so it can be passed through to a virtual machine.

1. Enable IOMMU in the Kernel

Edit GRUB:

$ sudo nano /etc/default/grub

Intel CPUs
GRUB_CMDLINE_LINUX="intel_iommu=on iommu=pt"

AMD CPUs
GRUB_CMDLINE_LINUX="amd_iommu=on iommu=pt"


Regenerate GRUB:

$ sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg


Reboot:

$ sudo reboot


Verify IOMMU:

$ dmesg | grep -i iommu


Example output:

DMAR: IOMMU enabled

2. Identify GPU & PCI IDs

List PCI devices:

$ lspci -nn


Example output:

01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GA107M [GeForce RTX 3050 Mobile] [10de:25a2] (rev a1)
01:00.1 Audio device [0403]: NVIDIA Corporation GA107 High Definition Audio Controller [10de:2291] (rev a1)


Extract IDs:

10de:25a2
10de:2291

3. Bind GPU to VFIO

Create VFIO configuration:

$ sudo nano /etc/modprobe.d/vfio-pci.conf

options vfio-pci ids=10de:25a2,10de:2291


Verify file:

$ cat /etc/modprobe.d/vfio-pci.conf

4. Load VFIO Before NVIDIA Drivers

Create soft dependency file:

$ sudo nano /etc/modprobe.d/nvidia-vfio-softdep.conf

softdep nvidia pre: vfio-pci
softdep nvidia_drm pre: vfio-pci


Verify:

$ cat /etc/modprobe.d/nvidia-vfio-softdep.conf

5. Add VFIO Drivers to Initramfs

Create dracut config:

$ sudo nano /etc/dracut.conf.d/vfio.conf

add_drivers+=" vfio vfio_iommu_type1 vfio_pci "


Verify:

$ cat /etc/dracut.conf.d/vfio.conf

6. Regenerate Initramfs
$ sudo dracut -f
$ sudo reboot

7. Verify VFIO Binding

Check driver usage:

$ lspci -nnk | grep -A3 -E "VGA|Audio"


Expected output:

Kernel driver in use: vfio-pci


Check VFIO modules:

$ lsmod | grep vfio

8. Common Issues
GPU still bound to nvidia
$ lsmod | grep nvidia


Fixes:

Verify PCI IDs

Disable Secure Boot

Re-run dracut -f

Reboot

No IOMMU output
$ dmesg | grep -E "DMAR|AMD-Vi"


Check BIOS virtualization settings.

Quick Status Check
$ dmesg | grep -i iommu
$ lspci -nnk | grep -A3 VGA


✔ IOMMU enabled
✔ GPU bound to vfio-pci

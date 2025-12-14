<h2>
  Table of Contents
</h2>

* [Introduction](#introduction)
* [Hardware Requirements](#hardware-requirements)
* [Tutorial](#tutorial)
  * [Part 1: Hardware Requirements](#part-1-hardware-requirements)
  * [Part 2: Enable IOMMU](#part-2-enable-iommu)
  * [Part 3: Creating the VM](#part-3-creating-the-vm)
  * [Part 4: Improving VM Performance](#part-4-improving-vm-performance)
  * [Part 5: Benchmarks](#part-5-benchmarks)
  * [Part 6: Software Licensing Considerations](#part-6-software-licensing-considerations)

---

<h2 id="introduction">
  Introduction
</h2>

This repository contains a complete, tested guide for setting up
**GPU passthrough on Fedora laptops** using **KVM, QEMU, and VFIO**.

### What This Guide Covers

- Fedora host setup
- Laptop-specific VFIO issues
- IOMMU and GPU isolation
- libvirt and virt-manager configuration

---

<h2 id="hardware-requirements">
  Hardware Requirements
</h2>

- **CPU with IOMMU support**
  - Intel: VT-d
  - AMD: AMD-Vi (SVM + IOMMU)
- **Two GPUs**
  - Integrated GPU (Intel/AMD) → host
  - Dedicated GPU (NVIDIA/AMD) → virtual machine
- UEFI firmware
- Secure Boot disabled
- External monitor (recommended for laptops)

---

<h2 id="tutorial">
  Tutorial
</h2>

<h3 id="part-1-hardware-requirements">
  Part 1: Hardware Requirements
</h3>

Verify your system meets all requirements before continuing.

---

<h3 id="part-2-enable-iommu">
  Part 2: Enable IOMMU
</h3>

This section configures the kernel and firmware to enable IOMMU support.

---

<h3 id="part-3-creating-the-vm">
  Part 3: Creating the VM
</h3>

Create a UEFI-based virtual machine using QEMU and libvirt.

---

<h3 id="part-4-improving-vm-performance">
  Part 4: Improving VM Performance
</h3>

Optimize CPU, memory, and display performance.

---

<h3 id="part-5-benchmarks">
  Part 5: Benchmarks
</h3>

Compare native vs virtualized GPU performance.

---

<h3 id="part-6-software-licensing-considerations">
  Part 6: Software Licensing Considerations
</h3>

Understand Windows licensing and activation in virtual machines.

### Guide to Implementing KernelSU-Next with SUSFS for Non-GKI MSM-4.14 Kernels  
*Authored by Khaliq (Morpheus)*  

This guide provides detailed steps to integrate **KernelSU-Next** with **SUSFS** for **non-GKI MSM-4.14 kernels**. Follow these instructions carefully to ensure a successful implementation.

---

### Initial Setup
1. **Navigate to the custom ROM source directory**:  
   ```bash
   cd /path/to/custom_rom_source
   ```

2. **Enter the kernel source directory**:  
   ```bash
   cd kernel/google/msm-4.14
   ```

---

### Implementation Steps
1. **Run the KernelSU-Next setup script**:  
   This step downloads and initializes the KernelSU-Next environment.
   
   • Next-susfs-msm-4.14 branch
   ```bash
   curl -LSs "https://raw.githubusercontent.com/Bias8145/KernelSU-Next/next-susfs-4.14/kernel/setup.sh" | bash -s next-susfs-4.14
   ```

2. **Clone the SUSFS repository for kernel 4.14**:  
   This repository contains additional patches and files necessary for SUSFS integration.  
   ```bash
   git clone https://gitlab.com/simonpunk/susfs4ksu.git -b kernel-4.14
   ```

3. **Copy SUSFS patches to the kernel directory**:  
   The files required for SUSFS integration are stored in the `susfs4ksu` repository.  
   ```bash
   cp -v susfs4ksu/kernel_patches/fs/* fs
   cp -v susfs4ksu/kernel_patches/include/linux/* include/linux
   ```

4. **Apply the additional SUSFS patch**:  
   This step ensures proper integration of SUSFS with the kernel.  
   ```bash
   cp -v susfs4ksu/kernel_patches/50_add_susfs_in_kernel-4.14.patch .
   patch -p1 < 50_add_susfs_in_kernel-4.14.patch
   ```

5. ***Compile or build the kernel***

---

### Conclusion  
By following these steps, you have successfully implemented **KernelSU-Next** with **SUSFS** on a **non-GKI MSM-4.14 kernel**. Ensure you compile the kernel and test it thoroughly to verify functionality.  

*This guide is brought to you by Khaliq (Morpheus), inspired by the Greek god of dreams.*

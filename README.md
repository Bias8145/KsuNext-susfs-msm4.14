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
   ```bash
   curl -LSs "https://raw.githubusercontent.com/rifsxd/KernelSU-Next/next/kernel/setup.sh" | bash -s v1.0.3
   ```

2. **Enter the KernelSU-Next directory**:  
   ```bash
   cd KernelSU-Next/
   ```

3. **Download the SUSFS v1.5.3 patch**:  
   This patch implements the SUSFS functionality.  
   ```bash
   curl -o 0001-Kernel-Implement-SUSFS-v1.5.3.patch https://github.com/sidex15/KernelSU-Next/commit/1e750de25930e875612bbec0410de0088474c00b.patch
   ```

4. **Apply the SUSFS v1.5.3 patch**:  
   ```bash
   patch -p1 < 0001-Kernel-Implement-SUSFS-v1.5.3.patch
   ```
5. **Back to kernel source directory**:
   ```bash
   cd ..
   ```

6. **Clone the SUSFS repository for kernel 4.14**:  
   This repository contains additional patches and files necessary for SUSFS integration.  
   ```bash
   git clone https://gitlab.com/simonpunk/susfs4ksu.git -b kernel-4.14
   ```

7. **Copy SUSFS patches to the kernel directory**:  
   The files required for SUSFS integration are stored in the `susfs4ksu` repository.  
   ```bash
   cp -v susfs4ksu/kernel_patches/fs/* fs
   cp -v susfs4ksu/kernel_patches/include/linux/* include/linux
   ```

8. **Apply the additional SUSFS patch**:  
   This step ensures proper integration of SUSFS with the kernel.  
   ```bash
   cp -v susfs4ksu/kernel_patches/50_add_susfs_in_kernel-4.14.patch .
   patch -p1 < 50_add_susfs_in_kernel-4.14.patch
   ```

---

### Conclusion  
By following these steps, you have successfully implemented **KernelSU-Next** with **SUSFS** on a **non-GKI MSM-4.14 kernel**. Ensure you compile the kernel and test it thoroughly to verify functionality.  

*This guide is brought to you by Khaliq (Morpheus), inspired by the Greek god of dreams.*

# OPlus MT6853 Universal Kernel Project

![Kernel Version](https://img.shields.io/badge/Kernel-4.14.336%2B-blue.svg)
![Target-Android](https://img.shields.io/badge/Android-12%20%7C%2013-green.svg)
![Platform](https://img.shields.io/badge/Platform-MT6853-orange.svg)

针对 OPPO/Realme MT6853 (Dimensity 720/800U) 平台的通用高性能内核。本项目通过深度回写（Backport）现代内核特性并移植 OEM 优化补丁，完美适配 Android 12 及更高版本的系统需求。

---

## 📱 支持设备清单
本内核采用通用配置，支持以下基于 OPlus 底层的 MT6853 机型：
* **OPPO 系列**: A72 5G, A53 5G, K7x, A95 5G, Reno4 SE
* **Realme 系列**: Q2, Q2 Pro, Q2i, V5 5G, V15 5G, X7 5G

## 🚀 核心改进

### ⚙️ 内核基础与存储优化
* **LTS 更新**: 同步至 Linux 官方稳定版 **4.14.336+**。
* **Xiaomi F2FS 移植**: 从小米高性能内核移植了 F2FS 驱动，修复了多处内存泄露（checkpoint.c）并优化了数据映射（data.c）与直连 I/O（DIO）性能。
* **LZ4 加速**: 升级了 LZ4 压缩库，引入 `__builtin_memcpy` 优化，大幅提升文件系统解压速度及应用启动加载速度。
* **TCP BBR**: 开启并默认启用 Google **BBR** 拥塞控制算法，显著提升移动网络环境下的数据传输速度与稳定性。

### 🔗 eBPF & 存储适配 (Android 12+)
* **BPF Backport**: 完整移植了高版本内核的 eBPF 支撑框架，解决 Android 12+ 上的网络统计、流量限制（Tethering）和防火墙兼容性问题。
* **path_umount**: 回写了 `path_umount` 函数，增强了存储挂载点卸载的稳定性，确保 Android 12+ 存储沙盒机制正常运行。
* **安全性修复**: 适配了 `get_cred_rcu` 的原子操作类型，修复了 `bpf_verifier_vlog` 的溢出问题。

### 🛠️ 附加驱动与功能
* **ReSukiSU**: 内置高度定制的 Root 权限支持（基于 KernelSU 兼容层）。
* **Xiaomi sdFAT**: 引入小米高性能 sdFAT 驱动，大幅优化大容量 SD 卡的挂载速度与 exFAT 性能。

## 🛠️ 编译说明

### 1. 环境准备
```bash
sudo apt-get install build-essential bc libncurses5-dev libc6-i386 lib32ncurses5-dev lib32z1

# 🚀 MT6853 Kernel (OPPO / Realme) - Android 12

![Kernel Version](https://img.shields.io/badge/Kernel-4.14.x-blue.svg)
![Android Version](https://img.shields.io/badge/Android-12-green.svg)
![Platform](https://img.shields.io/badge/Platform-MediaTek%20MT6853-orange.svg)
![Build](https://img.shields.io/github/actions/workflow/status/momo54181/android_kernel_oplus_mt6853/build.yml)

---

这是一个针对 **OPPO / Realme (MediaTek MT6853 / Dimensity 720)** 平台打造的 Android 12 Linux 4.14 内核源码仓库。

本项目基于 OPlus 官方内核源码进行维护，并集成：

- ReSukiSU 内核特权框架
- GitHub Actions 自动化 CI/CD
- AnyKernel3 自动刷包生成

支持通过 GitHub Actions 自动编译、打包并发布 Release。

---

# 📱 支持设备

本内核采用通用 MT6853 OPlus 平台配置：

## OPPO

- OPPO A72 5G
- OPPO A53 5G
- OPPO K7x
- OPPO A95 5G
- OPPO Reno4 SE


## Realme

- realme Q2
- realme Q2 Pro
- realme Q2i
- realme V5 5G
- realme V15 5G
- realme X7 5G
- realme 7 5G
- realme Narzo 30 Pro 5G


---

# ✨ Features

## 🔧 ReSukiSU

内置：

- **ReSukiSU Kernel Integration**

无需手动 Patch 内核，即可获得内核级权限管理能力。


项目地址：

https://github.com/ReSukiSU/ReSukiSU


---

## ⚡ 自动 CI 编译

通过 GitHub Actions 自动完成：

- 编译环境部署
- GCC / Clang 下载
- 内核编译
- AnyKernel3 打包
- Release 发布


生成文件：

```
MT6853-xxx-AnyKernel3.zip
```

可直接通过：

- TWRP
- OrangeFox
- 其他支持 AnyKernel3 的 Recovery

刷入。


---

# 🌿 Branch 编译规则

项目支持多分支编译：

| Branch | Clang |
|-|-|
| kernel-main | Android NDK r28c Clang |
| kernel-dev | Android NDK r28c Clang |
| vanilla | crDroid Clang 11 |
| vanilla-* | crDroid Clang 11 |
| 其他 | Android NDK r28c Clang |


GitHub Actions 会根据分支名称自动选择对应工具链。

例如：

```
kernel-main
        ↓
clang19


vanilla-test
        ↓
clang11
```


---

# 🛠 Toolchains

编译环境：

```
Ubuntu 22.04 LTS
```


## Clang

默认：

```
Android NDK r28c Clang
```

用于：

```
kernel-main
kernel-dev
```


Vanilla 分支：

```
crDroid clang-6443078
```

用于：

```
vanilla*
```


源码：

https://github.com/crdroidandroid/android_prebuilts_clang_host_linux-x86_clang-6443078


---

## GCC

32/64 位交叉编译：

```
aarch64-linux-android-4.9
arm-linux-androideabi-4.9
```

版本：

```
android-12.1.0_r27
```


---

## Kernel Config

默认：

```
mo-mt6853_defconfig
```


---

# 💻 Local Build Guide


## 1. Clone


普通版本：

```bash
git clone -b kernel-main \
https://github.com/momo54181/android_kernel_oplus_mt6853 \
android-kernel

cd android-kernel
```


Vanilla：

```bash
git clone -b vanilla \
https://github.com/momo54181/android_kernel_oplus_mt6853 \
android-kernel

cd android-kernel
```


---

# 2. 设置编译器


## kernel-main / kernel-dev


使用：

```
NDK r24 Clang
```


例如：

```bash
export PATH=/path/to/clang19/bin:/path/to/gcc64/bin:/path/to/gcc32/bin:$PATH
```



## vanilla 分支


使用：

```
crDroid clang11
```


例如：

```bash
export PATH=/path/to/clang11/bin:/path/to/gcc64/bin:/path/to/gcc32/bin:$PATH
```


---

# 3. 生成配置


```bash
make \
-s \
O=out \
ARCH=arm64 \
mo-mt6853_defconfig
```


---

# 4. 开始编译


```bash
make \
-j$(nproc --all) \
O=out \
ARCH=arm64 \
CC="clang" \
LLVM_IAS=1 \
CLANG_TRIPLE=aarch64-linux-gnu- \
CROSS_COMPILE=aarch64-linux-android- \
CROSS_COMPILE_ARM32=arm-linux-androideabi- \
LD=ld.lld
```


---

# 📦 输出文件


编译完成：

Kernel Image:

```
out/arch/arm64/boot/Image.gz-dtb
```


AnyKernel3:

```
MT6853-branch-AnyKernel3.zip
```


---

# 🤖 GitHub Actions 使用


进入：

```
Actions
 ↓
MT6853-Kernel-A12
 ↓
Run workflow
```


输入：

```
branch:
kernel-main
```


或者：

```
branch:
vanilla
```


Actions 会自动：

1. 拉取指定分支
2. 判断 Clang 版本
3. 编译内核
4. 制作 AnyKernel3
5. 发布 Release


---

# 📜 License

本项目仅用于学习、研究 Android Kernel 开发。

所有版权归原始项目作者及相关厂商所有。

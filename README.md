# STM32-Linux-Dev-Env
抛弃 Keil！STM32 在 Linux 下的纯手工命令行开发环境搭建指南

# 抛弃 Keil！STM32 在 Ubuntu 下的纯命令行开发环境搭建指南

作为一个习惯了掌握底层逻辑的开发者，受够了 Windows 下 Keil 臃肿的界面和高度绑定的工具链。这篇文档记录了我如何将 STM32 开发环境全面迁移到 Linux (Ubuntu)，实现 VS Code + Makefile + GCC 的纯手工极客工作流。

## 1. 核心思路：向 CubeMX “借”底层
我们不使用 CubeMX 生成臃肿的业务代码，只用它来精准提取以下三个最核心的底层文件：
* `startup_stm32f103xb.s` (启动文件)
* `STM32F103XX_FLASH.ld` (链接脚本)
* HAL 库与 CMSIS 核心驱动

## 2. 打造纯净的“黄金模板” (Golden Template)
经过精简，我将工程结构改造为以下分类，将官方库与手写代码（BSP）彻底分离：
（这里可以写一下我们建立的 `Core`、`Drivers/BSP` 结构）

## 3. 注入灵魂：自动化 Makefile 改造
原生的 Makefile 每次加文件都要手动改？不行。我将其改造为自动扫描 `.c` 文件的智能模式：
（在这里贴上你修改过的那段 `C_SOURCES = $(wildcard ...)` 的代码）

## 4. 补齐 VS Code 极客配置
为了拥有代码跳转和一键编译烧录体验，在 `.vscode` 文件夹中配置了三个核心文件：
* `c_cpp_properties.json`：解决头文件波浪线
* `tasks.json`：绑定 `make -j4` 快捷编译
* `launch.json`：绑定 OpenOCD 调试
（可以选择性地把你的 JSON 代码贴上来）

## 5. 终极大招：一键生成工程 Shell 脚本
为了彻底告别“复制粘贴”，我写了一个全局 Shell 脚本。只需在终端敲入 `new_stm32 <项目名>`，一秒钟内即可拉取黄金模板、自动重命名目标文件、甚至自动完成首次 Git 提交。

（在这里贴上你那个超牛的 `new_stm32` 脚本代码！）

## 总结
脱离 IDE 的舒适区，虽然初期会遇到找不着命令的痛苦，但真正打通任督二脉后，这种对代码从编译到链接拥有 100% 掌控力的感觉，才是真正属于工程师的浪漫！

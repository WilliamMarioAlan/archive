# wsl2（windows subsystem linux)

**Cygwin** 和 **WSL (Windows Subsystem for Linux)** 是两种使 Windows 用户能够运行类 Unix/Linux 环境的技术。它们提供了不同的方式来在 Windows 系统上使用 Linux 命令行工具、脚本和应用程序。以下是对这两者的详细比较：

---

### **Cygwin vs. WSL**

| **特性** | **Cygwin** | **WSL (Windows Subsystem for Linux)** |
| --- | --- | --- |
| **核心技术** | 模拟 Unix 系统调用 | 通过虚拟化技术运行 Linux 内核 |
| **兼容性** | 模拟 Linux 环境，部分工具可能不兼容 | 完全兼容 Linux 应用程序和工具 |
| **性能** | 较低，依赖模拟层 | 高，接近原生 Linux 性能 |
| **集成度** | 与 Windows 集成较少，主要依赖命令行工具 | 与 Windows 更加紧密集成，支持双向文件系统访问 |
| **安装难度** | 稍复杂，需要手动安装和配置工具 | 简单，直接从 Microsoft Store 安装发行版 |
| **图形界面支持** | 不支持（需额外配置） | WSLg 提供原生图形界面支持 |
| **适用场景** | 适合运行 Linux 工具，轻量级开发环境 | 适合开发者、跨平台开发、容器化应用开发 |

### **总结**

- **Cygwin**：适合那些只需要在 Windows 上运行少量 Unix 工具的用户，尤其是当你不需要完整的 Linux 内核时。它是一个轻量级的解决方案，适合用于较老的 Windows 系统，或者在需要使用某些 Linux 工具但不需要完整 Linux 环境的场合。
- **WSL**：是当前在 Windows 上运行 Linux 环境的最佳选择，特别是 WSL 2。它提供了接近原生 Linux 的性能和兼容性，并且集成度高，适合开发者、跨平台工作者以及需要完整 Linux 环境的用户。尤其是 WSLg 的图形界面支持，使得 WSL 成为运行 Linux 应用程序的非常强大且高效的工具。

如果你经常需要在 Windows 上开发 Linux 应用，或者需要运行 Docker、Kubernetes 等容器化环境，WSL 2 无疑是更合适的选择。而如果你只是偶尔需要一些 Linux 工具，Cygwin 仍然是一个有效的工具。

### 步骤 1：确认 Windows 版本

1. 确保你的 Windows 11 版本支持 WSL 2。通常，Windows 11 的版本已经包含对 WSL 2 的支持，因此可以跳过手动安装某些组件的步骤。

### 步骤 2：启用虚拟化

WSL 2 需要虚拟化支持，因此需要确保你的 BIOS/UEFI 设置中启用了虚拟化技术（Intel VT-x 或 AMD-V）。具体方法如下：

1. 重启电脑，进入 BIOS/UEFI 设置界面（通常是按 **F2** 或 **DEL** 键）。
2. 查找虚拟化选项（如 Intel VT-x 或 AMD-V）并启用。
3. 保存设置并退出 BIOS。

### 步骤 3：安装 WSL 和设置默认为 WSL 2

1. 打开 **PowerShell**（管理员权限）：
    - 右键点击开始按钮，选择 **Windows PowerShell（管理员）** 或 **终端（管理员）**。
2. 执行以下命令来安装 WSL（这个命令会自动启用 WSL 和安装 WSL 2）：
    
    ```powershell
    wsl --install
    
    ```
    
    这个命令将会：
    
    - 启用 WSL 和虚拟化平台。
    - 安装 **WSL 2** 作为默认版本。
    - 安装 **Ubuntu** 作为默认 Linux 发行版（你可以根据需要更换）。
3. **重启计算机**：安装完成后，你会被要求重启电脑。

### 步骤 4：安装 Linux 发行版

1. **打开 Microsoft Store**，搜索你希望安装的 Linux 发行版。常见的 Linux 发行版包括：
    - **Ubuntu**
    - **Debian**
    - **Kali Linux**
    - **Fedora**
    - **openSUSE**
2. 选择你想安装的发行版并点击 **安装**。
3. 安装完成后，从 **开始菜单** 启动 Linux 发行版（如 Ubuntu）。首次启动时，它会要求你设置一个 Linux 用户名和密码。

### 步骤 5：确认和设置默认版本为 WSL 2

如果你希望将所有已安装的发行版默认设置为 **WSL 2**，可以执行以下命令：

```powershell
wsl --set-default-version 2
```

此命令会确保任何后续安装的 Linux 发行版都会自动使用 **WSL 2**。

### 步骤 6：检查 WSL 版本和切换版本

1. **查看已安装的发行版和版本**：
    
    ```powershell
    wsl --list --verbose
    ```
    
    该命令会列出所有安装的 Linux 发行版及其对应的 WSL 版本，例如：
    
    ```
    NAME      STATE           VERSION
    * Ubuntu    Running         2
    
    ```
    
2. **将已安装的发行版从 WSL 1 切换到 WSL 2**：
    
    如果你已经安装了 Linux 发行版，并且它默认使用 WSL 1，你可以使用以下命令将其切换到 WSL 2：
    
    ```powershell
    wsl --set-version <发行版名称> 2
    
    ```
    
    例如，要将 Ubuntu 切换到 WSL 2：
    
    ```powershell
    wsl --set-version Ubuntu 2
    ```
    

### 步骤 7：使用 WSL 2

1. **启动你的 Linux 发行版**，例如从 **开始菜单** 中启动 **Ubuntu**。
2. 系统会要求你进行首次设置，创建一个 Linux 用户名和密码。

你现在就可以在 Windows 上通过 WSL 2 享受完整的 Linux 环境了。

### 步骤 8：访问 Windows 文件系统

你可以从 WSL 中访问 Windows 文件系统。Windows 的文件系统通过 `/mnt/c`、`/mnt/d` 等路径挂载在 Linux 子系统中。例如，`/mnt/c` 对应 Windows 的 C 盘，`/mnt/d` 对应 D 盘。

在 WSL 中输入以下命令即可访问 Windows 文件：

```bash
cd /mnt/c/Users/<你的用户名>/Documents

```

### 步骤 9：安装常用开发工具

你可以通过 `apt` 或其他包管理器来安装开发工具。例如：

```bash
sudo apt update
sudo apt install build-essential git python3 python3-pip

```

### 常见问题与解决方法

- **WSL 2 无法启动**：如果遇到启动问题，请检查是否启用了虚拟化，并确保 WSL 2 的内核已经安装。如果没有，尝试访问 [WSL 2 内核更新包下载页面](https://aka.ms/wsl2kernel) 并安装更新。
- **文件访问问题**：确保你没有权限问题，使用 `chmod` 或 `chown` 命令调整文件权限。
- **资源限制**：如果你遇到性能问题，可以通过修改 `.wslconfig` 文件来调整分配给 WSL 的内存和 CPU 核心数。

---

通过这些步骤，你应该可以在 Windows 11 上顺利安装和配置 WSL 2，享受一个高效的 Linux 开发环境。如果你遇到任何问题，随时告诉我，我会帮助你解决！
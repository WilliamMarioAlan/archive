# chsh -s /bin/bash(change the shell to bash修改bash)

chsh -s /bin/bash修改默认Shell

在类 Unix 系统中，`bash` 和 `sh` 是两种不同的 shell，它们虽然在许多方面相似，但也存在一些区别。通常，`sh` 是系统默认的标准 shell，而 `bash` 是一个功能更强大的 shell，常常用于开发和交互式使用。

如果你希望将 `bash` 设置为默认的 shell 而不是 `sh`，可以通过以下方法进行配置。

---

### **1. 检查当前默认 shell**

首先，检查当前的默认 shell：

```bash
echo $SHELL
```

如果输出是 `/bin/sh` 或类似内容，那么当前的默认 shell 是 `sh`。

---

### **2. 修改默认 shell**

### **方法一：使用 `chsh` 命令**

`chsh`（change shell）命令可以用于更改用户的默认 shell。

1. 确定 `bash` 的路径：
运行以下命令，查找 `bash` 的安装路径（通常是 `/bin/bash` 或 `/usr/bin/bash`）：
    
    ```bash
    which bash
    ```
    
2. 更改默认 shell：
使用 `chsh` 命令将默认 shell 设置为 `bash`：
    
    ```bash
    chsh -s /bin/bash
    ```
    
    - 如果 `bash` 的路径不同，请根据你的实际情况修改路径。
3. 退出并重新登录：
修改后，需要退出当前会话并重新登录，或者重新启动终端，以使更改生效。

### **方法二：手动编辑 `/etc/passwd` 文件**

如果你无法使用 `chsh` 命令，或者需要为多个用户设置默认 shell，可以手动编辑 `/etc/passwd` 文件。

1. 打开 `/etc/passwd` 文件：
    
    ```bash
    sudo nano /etc/passwd
    ```
    
2. 找到你的用户行，通常形如：
    
    ```
    username:x:1000:1000:User Name:/home/username:/bin/sh
    
    ```
    
3. 将最后的 `/bin/sh` 改为 `/bin/bash`，例如：
    
    ```
    username:x:1000:1000:User Name:/home/username:/bin/bash
    
    ```
    
4. 保存并退出编辑器（在 `nano` 中按 `Ctrl+O` 保存，`Ctrl+X` 退出）。
5. 重新登录或重启系统。

---

### **3. 临时使用 `bash`**

如果你只想在当前终端会话中使用 `bash`，可以直接运行：

```bash
bash

```

这会启动一个新的 `bash` 会话，但不会修改默认 shell 配置。

---

### **4. 确认更改**

重新登录后，运行以下命令确认是否成功切换到 `bash`：

```bash
echo $SHELL

```

如果返回 `/bin/bash`，则说明默认 shell 已更改为 `bash`。

---

### **总结**

- 使用 `chsh -s /bin/bash` 是最简便的方式来更改默认 shell。
- 如果没有权限使用 `chsh` 命令，可以编辑 `/etc/passwd` 文件来手动更改。
- 更改默认 shell 后，需要重新登录才能生效。
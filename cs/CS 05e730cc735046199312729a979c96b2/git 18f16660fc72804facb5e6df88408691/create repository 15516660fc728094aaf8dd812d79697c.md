# create repository

- **Git**: 从 [Git官网](https://git-scm.com/) 下载并安装。
- **GitHub账户**: 创建一个 GitHub 账号并完成必要设置。
- **SSH密钥**:
    - 生成SSH密钥并添加到 GitHub:
        
        ```bash
        ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
        ssh-add ~/.ssh/id_rsa
        cat ~/.ssh/id_rsa.pub
        ```
        
    - 将生成的公钥添加到 GitHub (个人设置 -> SSH and GPG keys)。

---

## **2. 创建一个仓库**

### **2.1 在 GitHub 上创建仓库**

1. 登录 GitHub。
2. 点击 `New Repository`。
3. 填写仓库名、描述，可选择初始化仓库（添加 README、LICENSE 等）。

### **2.2 本地克隆仓库**

- 如果在 GitHub 初始化了仓库：
    
    ```bash
    git clone git@github.com:your_username/repository_name.git
    ```
    
- 如果没有初始化：
    
    ```bash
    mkdir repository_name && cd repository_name
    git init
    git remote add origin git@github.com:your_username/repository_name.git
    
    ```
    

---

## **3. 基本操作**

### **3.1 添加文件**

- 创建文件/文件夹。
    
    ```bash
    echo "# Project Title" > README.md
    mkdir src
    touch src/main.py
    ```
    
- 添加文件到 Git 暂存区：
    
    ```bash
    git add .
    ```
    

### **3.2 提交更改**

```bash
git commit -m "Initial commit"
```

### **3.3 推送到 GitHub**

```bash
git branch -M main  #-M: 强制重命名分支。如果新分支名已经存在，-M 会覆盖它（而不需要先删除已有分支）。 这样可以确保主分支是 main
git branch  #查看当前分支
git branch -r #查看远程仓库分支
git branch -a # 列出所有分支（本地+远程）
git push -u origin main
```

---
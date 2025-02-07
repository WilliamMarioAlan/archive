# git fetch && git pull

### Q1: `git fetch` 和 `git pull` 如何使用？

- **`git fetch`**：这个命令用于从远程仓库获取最新的提交，但不会自动合并到本地的分支。它相当于更新本地的远程追踪分支信息，使得本地仓库的历史记录跟远程仓库保持同步。
    
    使用方法：
    
    ```bash
    git fetch <远程仓库名> <远程分支名>
    
    ```
    
    或者获取所有分支的更新：
    
    ```bash
    git fetch --all
    
    ```
    
    例如：
    
    ```bash
    git fetch origin
    
    ```
    
    这会获取 `origin` 远程仓库的所有更新，但不会更改本地的代码。
    
- **`git pull`**：这个命令会执行 `git fetch` 获取远程更新，然后执行 `git merge`（或者根据配置执行 `git rebase`）将远程更新合并到当前本地分支。它是一种更加直接的操作，相当于 `git fetch` + `git merge`。
    
    使用方法：
    
    ```bash
    git pull <远程仓库名> <远程分支名>
    
    ```
    
    例如：
    
    ```bash
    git pull origin main
    
    ```
    
    这会将 `origin` 远程仓库的 `main` 分支合并到当前分支。
    

### Q2: `git fetch` 后面是否需要加主分支名字？`git pull` 后面是否需要加主分支名字？

- **`git fetch` 后是否加主分支名字**：
通常情况下，`git fetch` 后面不需要指定分支名，它会获取远程仓库所有分支的更新。如果你只关心某个特定分支的更新，可以加上远程仓库和分支名，如：
    
    ```bash
    git fetch origin main
    
    ```
    
- **`git pull` 后是否加主分支名字**：
是的，如果你想将远程的主分支（通常是 `main` 或 `master`）拉取到当前分支，你需要指定远程仓库和分支名。例如：
    
    ```bash
    git pull origin main
    
    ```
    
    如果你不指定分支名，Git 会尝试拉取当前分支的默认远程分支（通常是与当前分支关联的远程分支）。如果你不确定当前分支的远程追踪分支，可以通过 `git branch -vv` 查看。
    

总结：

- `git fetch` 默认会拉取所有分支，除非指定远程和分支名。
- `git pull` 通常需要指定远程仓库和分支名，尤其是在你想拉取的远程分支不是当前分支的默认追踪分支时。
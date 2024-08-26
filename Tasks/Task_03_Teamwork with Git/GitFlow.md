### 1. **项目初始化**

- **步骤**：创建一个新的 Git 仓库，初始化主分支（master/main）和开发分支（develop）。

- Git 命令

  ：

  ```
  bash复制代码# 创建一个新的 Git 仓库
  git init
  
  # 添加所有文件并进行第一次提交
  git add .
  git commit -m "Initial commit"
  
  # 创建 develop 分支
  git checkout -b develop
  
  # 推送到远程仓库（例如 GitHub 或 GitLab）
  git remote add origin <remote_repository_url>
  git push -u origin master
  git push -u origin develop
  ```

### 2. **功能开发**

- **步骤**：根据需求创建功能分支（feature 分支），在功能分支上进行开发，开发完成后合并回开发分支。

- Git 命令

  ：

  ```
  bash复制代码# 从 develop 分支创建一个新的 feature 分支
  git checkout develop
  git checkout -b feature/your-feature-name
  
  # 进行代码开发，定期提交
  git add .
  git commit -m "Add feature description"
  
  # 功能开发完成后，合并回 develop 分支
  git checkout develop
  git merge --no-ff feature/your-feature-name
  
  # 删除本地 feature 分支
  git branch -d feature/your-feature-name
  
  # 推送 develop 分支到远程仓库
  git push origin develop
  ```

### 3. **版本发布**

- **步骤**：当准备发布新版本时，从开发分支创建发布分支（release 分支），在发布分支中完成最后的调试和文档更新等工作，确认无误后将其合并到主分支，并打上版本标签。

- Git 命令

  ：

  ```
  bash复制代码# 从 develop 分支创建 release 分支
  git checkout develop
  git checkout -b release/1.0.0
  
  # 完成调试和文档更新等，提交更改
  git add .
  git commit -m "Prepare release 1.0.0"
  
  # 合并 release 分支到 master 分支
  git checkout master
  git merge --no-ff release/1.0.0
  
  # 给 master 分支打上标签
  git tag -a 1.0.0 -m "Release version 1.0.0"
  
  # 将 master 分支推送到远程仓库，包括标签
  git push origin master
  git push origin 1.0.0
  
  # 将 release 分支合并回 develop 分支
  git checkout develop
  git merge --no-ff release/1.0.0
  
  # 删除本地和远程 release 分支
  git branch -d release/1.0.0
  git push origin --delete release/1.0.0
  ```

### 4. **修复问题**

- **步骤**：当在生产环境中发现严重的 bug 时，可以创建修复分支（hotfix 分支），在该分支中修复问题后，合并到主分支和开发分支，并更新版本号。

- Git 命令

  ：

  ```
  bash复制代码# 从 master 分支创建 hotfix 分支
  git checkout master
  git checkout -b hotfix/1.0.1
  
  # 修复问题，提交修复代码
  git add .
  git commit -m "Fix critical issue"
  
  # 合并 hotfix 分支到 master 分支
  git checkout master
  git merge --no-ff hotfix/1.0.1
  
  # 更新版本号并打上标签
  git tag -a 1.0.1 -m "Release version 1.0.1"
  
  # 将 master 分支推送到远程仓库，包括标签
  git push origin master
  git push origin 1.0.1
  
  # 将 hotfix 分支合并回 develop 分支
  git checkout develop
  git merge --no-ff hotfix/1.0.1
  
  # 删除本地和远程 hotfix 分支
  git branch -d hotfix/1.0.1
  git push origin --delete hotfix/1.0.1
  ```

### 5. **持续完善**

- **步骤**：重复功能开发、版本发布和修复问题的步骤，持续更新和完善项目。每次发布新版本时都遵循 Gitflow 的工作流，确保分支管理有序，代码质量稳定。
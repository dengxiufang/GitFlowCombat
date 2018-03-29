### gitflow 工作流程

* 项目负责人在本地master基础上创建一个 develop 分支,推送到服务器
```git
git branch develop
git push -u origin develop
```
* 其他开发人员，需要克隆 develop 中央仓库的源码，创建一个 develop 的轨迹版本，
如果已经克隆过项目，则，不需要执行以下第一条命令
```git
git clone git@github.org:search-cloud/demo.git
git checkout -b develop origin/develop
```
develop 这个分支将包含这个项目的完整历史记录，而master将包含缩略版本


### 新功能开发流程
#### 新建feature分支
* 其他开发者走下面流程
* 下面开始基于 develop 分支创建新功能分支
```git
git checkout -b feature/demo develop
```
* 推送到远程仓库，共享
```git
git push
git push --set-upstream origin feature/demo
```
* 所有开发此新功能的人员，都要在此分支上开发提交代码
```git
git status
git add
git commit -m "Add some-file"
```
#### 完成新功能开发(合并feature分支到develop)
* 当确定新功能开发完成，且联调测试通过，并且新功能负责人已经得到合并feature分支到develop分支的允许；
这样才能合并feature分支到develop。
```git
git pull origin develop
git checkout develop
git merge feature/demo
git push
git branch -d feature/demo
```
**注意事项:新功能分支，永远不要直接合并到master分支**
**注意事项:合并可能会有冲突，应该谨慎处理冲突**
#### 在测试环境发布develop分支代码(提交测试)
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

### 线上版本发布流程
#### 从develop中创建准备发布的release分支
* 当主测试流程完成，源码已趋近于稳定状态，应该准备一个发布版本，确立版本号:
```git
git checkout -b rease-0.1.0 develop

git push
```
* 这个分支是清理准备发布、 整体回归测试、 更新文档，和做其他任何系统即将发布的事情。
#### 继续改 BUG
#### release分支合并到master发布
* 一旦已经满足发布条件（或已经到了预定发布日期），
应该把release分支合并到master分支和develop分支中，
然后，使用master发布新版本。合并release分支到develop分支是很重要的，
要让release上修改的东西能在后续的开发分支中生效。
```git
git checkout master
git merge release-0.1.0
git push
```
#### release分支合并到develop
```git
git checkout develop
git merge release-0.1.0
git push
git branch -d release-0.1.0
```
#### 打标签
* Release分支在功能开发分支（develop）和公共发布版（master）中，充当一个缓冲的作用。
每当有源码合并到master中的时候，应该在master上打一个标签，以便后续跟踪查阅。
```git
git tag -a 0.1.0 RELEASE -m "Initial public release" master
git push --tags
```

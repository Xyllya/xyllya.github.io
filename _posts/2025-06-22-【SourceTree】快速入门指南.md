---
Title: 【SourceTree】快速入门指南
date: 2025-06-22 16:33 +0800
categories: [软件 | 环境 | 配置]
tags: [SourceTree, Git]
---

## 01/ 安装
    
- [官网](https://www.sourcetreeapp.com/)
- 安装 - 创建 Bitbucker 账户 - ssh密钥可暂时选否（后续通过git生成再添加进去）

## 02/ 关联远程仓库
    
1. SSH + 密钥
	- SourceTree添加SSH密钥：工具 - 选项 - 一般 - SSH客户端配置
		- SSH密钥：选择生成的密钥（C:\Users\xxxxx\.ssh\id_rsa.pub）
		- SSH客户端：OpenSSH
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506221045852.png)
2. HTTPS + 账号密码


## 03/ SourceTree设置默认工作目录

- 工具 - 选项 - 一般 - Repo Settings - 选择项目存储默认目录
	![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210903720.png)


## 04/ Clone仓库

- New tab - Clone
	- 原路径/URL：拉取项目的git路径
	- 目标路径：项目本地保存位置
	- 名字：项目名称（根据路径自动获取）
	![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210910224.png)


## 05/ 拉取，提交与推送

- 团队协作：一定要先拉取团队最新更新的代码再推送自己更新的代码 ⭐⭐⭐

- 拉取：从远程仓库获取信息并同步至本地仓库，并且自动执行合并（merge）操作，
  即 pull=fetch+merge
	- 仓库代码有了新的更改
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210946612.png)
	- 本地拉取以更新信息
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210943682.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210948539.png)
- 将本地的修改提交、推送至仓库
	- 1. 将修改的代码暂存到暂存区
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210954312.png)
	- 2. 将暂存的文件提交到本地仓库
		- 提交前添加备注 - 提交
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210956379.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210959267.png)
	- 3. 将本地仓库的修改代码推送至仓库
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506210959660.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211000084.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211001029.png)


## 06/ 分支切换，新建，合并

- 分支切换
	- 切换本地分支：直接双击分支
	- 切换远程分支：双击 - 检出该分支（或右键分支-检出）
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211017577.png)
		- 本地出现远端的新分支
- 新建分支
	- 需要在哪个主分支上新建分支就需要切换到对应的主分支，然后在主分支上创建分支。 eg.在 master 上创建 feature-0621分支
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211028571.png)
	- 向分支提交推送
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211031213.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211036537.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211036132.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211037920.png)
- 合并分支
	- 在合并代码之前我们都需要将需要合并的分支拉取到最新状态
	- 切换到主分支（最终合并到的分支）- 右键要合并的分支 - 合并feature-0621至当前分支。 eg.将feature-0621合并至master
		- 在master上右键feature-0621合并
			![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211042551.png)
		- 推送
			![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211045105.png)
			![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211045255.png)


## 07/ 代码冲突解决
    
- 产生冲突的原因
	- 1. 不同分支的合并：本地修改B分支的文件1后，将B分支推送到A分支，如果A分支的文件1也被修改，即产生冲突
	- 2. 同一分支的拉取或推送：本地修改文件1，此时远端的文件1也被修改了，本地和远端文件不一致，产生冲突
- 制造一个冲突
	- 远程仓库的 test1 添加了内容
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211119433.png)
	- 本地仓库 GiteeTest 也对 test1 做了修改
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211120369.png)
	- GiteeTest 没有拉取仓库更改的代码，直接提交推送，报错
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211123863.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211123960.png)
	- GiteeTest 拉取最新代码后遇见冲突
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211127535.png)
		- 冲突的内容
			![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211129831.png)
- 解决冲突
	- 1. 手动打开冲突文件解决冲突
		- 根据项目需求删除不需要的代码
		- 若都需要就删除 `<<<<<<< HEAD` 和 `>>>>>>> 0e5d01f67fd87cc5e5add9573e4fefcd790804e3` 等符号
	- 2. 使用外部文本文件对比工具 Beyond Compare 解决冲突
	- 3. 最后将冲突文件标记已解决，提交推送到远程仓库
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211353415.png)


## 08/ 贮藏

- 对于修改到一半，不能提交推送又急需完成其他分支可以将修改贮藏在本地
- 1. 暂存修改文件后贮藏
	![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211452656.png)
	![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211453862.png)
	![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211454997.png)
- 2. 取出贮藏的文件
	- 贮藏记录 - 右键 - 应用贮藏区：修改文件回到未暂存区
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506211458331.png)


## 09/ 撤销回滚
    
- 对于后悔提交的代码可以撤销回滚，但只能撤销回滚最近的一次提交。
	- 右键 - 回滚提交 - 多了一个 Revert 反向提交
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506221021672.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506221023653.png)
- 重新提交 撤销回滚后的代码
	- Revert 反向提交记录 右键 - 回滚提交
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506221028056.png)
		![](https://jxy-1306180768.cos.ap-shanghai.myqcloud.com/image/202506221034620.png)


## References

- [Sourcetree安装详细（最新版本）](https://blog.csdn.net/zqd_java/article/details/123681302)
- [【最全面】SourceTree使用教程详解（连接远程仓库，克隆，拉取，提交，推送，新建/切换/合并分支，冲突解决，提交PR）](https://www.cnblogs.com/Can-daydayup/p/13128633.html#_label3)
- [sourcetree的使用（克隆、提交、推送、获取、拉取、分支创建与合并、解决冲突、撤销回滚、回退版本）](https://blog.csdn.net/weixin_47342392/article/details/139478745)

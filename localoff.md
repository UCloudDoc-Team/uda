因本地盘方舟服务需要下线，故后续将不再支持本地盘方舟的开通。存量的本地盘方舟服务将升级为云盘快照服务。

## 升级内容包含如下：

【本地盘】升级为【SSD云盘】
本地盘的【方舟服务】升级为云盘的【快照服务】
计费相关：

  * 原有的方舟服务会被关闭，并且对数据方舟功能进行退费，并开启新的快照服务。
  * 此次为平滑升级，保持原有的价格0.4元/G/月不变，服务进行了升级更新。
  
相较于本地盘方舟，在相同的价格情况下，云盘快照服务提供了更长的备份时间。

## 升级优势：

 * 无IO争抢，具备三副本容灾能力，IO隔离以及数据快速迁移能力
 * 本地盘不支持扩容，云盘支持扩容能力
 * 移不会导致自动备份中断，具备恢复至原来本地盘的备份时间点能力
 * [备份策略服务](https://docs.ucloud.cn/usnap/ivas) 进行了全面升级
   * 本地盘方舟服务：开启磁盘连续数据保护功能，自动备份策略为12小时任意秒级备份，24小时的任意整点备份，3天内的任意零点备份
   * 云盘快照服务：开启【基础版】套餐，自动备份策略为24小时任意秒级备份，60小时的任意整点备份，15天内的任意零点备份，支持3个手动备份快照
   * 进行升级完成后，您可在【快照服务管理】-》【快照详情页】的【基本信息】卡片中，对您升级后的快照服务 进行策略修改，满足您更多样化的业务需求
   
![image](/images/backuprange.png)


## 本地盘方舟服务相关操作

### 本地盘方舟创建

1）控制台创建：【云主机】创建页面，开启【数据方舟】

![image](/images/localudkcreate.png)

2）API接口：调用CreateUHostInstance ，磁盘类型需要选择本地盘。标记开通参数：TimemachineFeature : Yes。

### 方舟关闭
1）控制台操作：【云主机】产品虚机资源 详情页，【磁盘与恢复】页，操作【关闭方舟】按钮

![image](/images/localdelete.png)

2）API接口：调用DegradeToNormalUHostInstance

### 本地盘快照创建

1）控制台创建：【云主机】产品虚机资源 详情页，【磁盘与恢复】页，点击【进入方舟】

![image](/images/createsnap.png)

2）API接口：CreateSnapshot/CreateUserVDiskSnapshot

## 云盘快照服务相关操作

### 云盘快照服务创建

1）控制台创建：【云主机】创建页面，开启【快照服务】，点击后面的编辑icon，可以修改快照服务的备份套餐。

![image](/images/udisksnapcreate.png)

2）API接口：调用CreateUHostInstance 磁盘类型需要选择云盘

标记开通参数：Disks.N.BackupType: SNAPSHOT，Disks.N.BackupMode选择某个快照服务套餐。

  Disks.N.BackupMode: 枚举值："Primer"：入门版；"Base"：基础版，"Enterprise"：企业版，"Ultimate"：旗舰版，"Custom"：自定义备份链；默认值："Primer"。

  Disks.N.CustomBackup.Journal: Disks.N.BackupMode为"Custom"时，进行设置, 以12小时秒级为基础进行倍数扩增，如12、24、36、48。

  Disks.N.CustomBackup.Hour: Disks.N.BackupMode为"Custom"时，进行设置, 以24小时级为基础进行倍数扩增，如24、48、72、96。

  Disks.N.CustomBackup.Day: Disks.N.BackupMode为"Custom"时，进行设置, 以5天级为基础进行倍数扩增，如5、10、15、20、25、30。

### 快照服务关闭

1）控制台操作：点击【快照服务管理页】，选择【关闭服务】

![image](/images/snapdelete.png)

2）API接口：调用DeleteSnapshotService

### 云盘快照创建

1）控制台创建：

【云盘管理】选中要创建快照的云盘资源，点击【创建快照】，会提示先开启快照服务，开通完成后会自动跳转至【快照服务管理】，进入刚开通的服务的详情页，创建快照。

已经开通快照服务的云盘，点击【创建快照】会直接创建，再去【快照服务管理】-> 【云盘快照】查看快照资源。

![image](/images/snapshotcreate1.png)
![image](/images/snapshotcreate2.png)

2）API接口：调用UDISK的接口CreateUDiskSnapshot


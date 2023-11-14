### Q：Linode Object Storage的计费标准是什么

A：Linode Object Storage 的固定费用为每月 5 美元，包括 250 GB 的存储空间。这个统一费率是按比例分配的，因此如果您在一个月的一小部分时间使用对象存储，您只需支付一小部分费用。例如，如果您在半个月内启用了 Object Storage 并使用了多达 250 GB 的存储空间，您将在月底支付 2.50 美元的费用。在前 250 GB 的基础上，每增加 1 GB 的存储费用为 0.02 美元，并且此使用量也根据使用时间按比例分配。



### Q：linode Object Storage的存储媒介是什么？是SSD吗？

A： 闪存(flash)和旋转(spinning)介质的组合

### Q：如何设置 linode Object Storage桶及文件 ACL 为 public-read

A：Linode Object Storage ACL 分为两部分，桶级别的ACL和文件级别的ACL。
```
展开说明：
关于桶级别的ACL有四种

1.Private（默认）
只有您可以列出、创建、覆盖和删除该Bucket中的对象

2.Authenticated Read
所有通过认证的对象存储用户都可以列出该桶中的对象，但只能进行创建、覆盖和删除操作

3.Public Read
每个人都可以列出此Bucket中的对象，但只有您可以创建、覆盖和删除它们

4.Public Read/Write
每个人都可以列出、创建、覆盖和删除该Bucket中的对象。不建议这样做

文件级别的ACL有三种
1.Private
只有您可以下载此对象

2.Authenticated Read
所有通过认证的对象存储用户都可以下载该对象

3.Public Read
每个人都可以下载这个对象

注:通级别ACL控制能否访问存储桶,文件级别控制能否访问文件内容

设置桶级别的ACL方式:
1.通过Linode Cloud Manager页面修改
登录Linode Cloud Manager -> 找到左侧菜单 Object Storage -> 点击具体的存储桶 -> 选择上方的Access标签 -> 修改对应的ACL级别并保存

2.通过LinodeAPI修改
参考文档：https://www.linode.com/docs/api/object-storage/#object-storage-bucket-access-update

设置文件的ACL方式：
1.通过Linode Cloud Manager页面修改
登录Linode Cloud Manager -> 找到左侧菜单 Object Storage -> 点击具体的存储桶 -> 选择文件点击 -> 修改对应的ACL级别并保存

2.通过LinodeAPI修改（只能单个修改）
参考文档：https://www.linode.com/docs/api/object-storage/#object-storage-object-acl-config-update

3.通过S3cmd修改（只能修改现有的所有文件并不能应用于后续添加的新文件）

安装配置s3cmd:
参考文档：https://www.linode.com/docs/products/storage/object-storage/guides/s3cmd/

使用文档中的命令一次性设置桶中所有文件为Public-read
参考文档：https://www.linode.com/community/questions/20759/how-can-i-change-all-existing-objects-in-my-bucket-to-public-or-private-using-s3

4.通过s3cmd设置存储桶策略（应用于现有及后续添加的所有文件）

首先参考方式3中的文档安装配置s3cmd

安装配置完成后编写适用于自身情况的存储桶策略并应用策略
参考文档：https://www.linode.com/docs/products/storage/object-storage/guides/bucket-policies/

特别注意：
如果需要设置为公共读取:请将Principle设置为"*"

若无法再次读取修改策略，请确认现有策略是否包含读取编辑的权限 `s3:PutBucketPolicy`/`s3:GetBucketPolicy`
s3cmd info s3://your-bucket-name
```
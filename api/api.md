### Q：如何获取创建的image的id

A：https://api.linode.com/v4/images 通过这个接口列出可用的image id，其中以private为前缀的是私有的镜像，其他的是linode公有的

### Q：调用Linode API创建服务器，响应结果中是否包含ID

A：包含。响应结果样例如下：

![image-20230830142838598](../picture/image-20230830142838598.png)



### Q 如何查看账号的customerID（账户的ID）

A： https://api.linode.com/v4/profile 传入账户的API token 即可

![image-20231027152139756](../image/image-20231027152139756.png)
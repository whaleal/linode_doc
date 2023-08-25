### Q: Linode服务器的磁盘默认类型是什么？

​       A: 所有的Linode都采用SSD存储



### Q: 服务器关机了是否还继续收费

A: 还会收费，直到删除了这个服务器



### Q: Transfer是包月流量吗？network是速度上限吗？如果超了怎么算？

A: transfer是包月流量 network是带宽 流量如果用超了包月的 超出部分1TB 5$

​	

### Q：Linode 现在有香港节点吗？后面会有香港节点吗?

A：现在没有香港节点，未来会有（明年）。



### Q： 如何通过自定义镜像创建服务器

A： 上传镜像到 linode

![image-20230713161044009](../picture/image-20230713161044009.png)

![image-20230713161236638](../picture/image-20230713161236638.png)

这里只支持上传.gz这一种格式的文件 



上传之后根据镜像进行创建

![image-20230714112610718](../picture/image-20230714112610718.png)

对于上传的镜像也可以通过linode api的形式创建服务器



### Q：如何更换服务器的ip

A：更换服务器的ip只能在同属于一个region的服务器之间进行，所以事先要准备好一个同region的服务器，然后与当前服务器进行IP Transfer

![image-20230814095403709](../picture/image-20230814095403709.png)

![image-20230814095948664](../picture/README.png)

内网与外网ip都可以进行transfer





### Q：Linode是否支持vyos操作系统

A：没有直接可以创建的镜像，也不能直接以上传的镜像创建，需要按照教程自己实现

[在linode上安装vyos](https://www.linode.com/community/questions/18630/how-do-i-install-vyos-on-my-linode)

[安装自定义镜像](https://www.linode.com/docs/products/compute/compute-instances/guides/install-a-custom-distribution/)


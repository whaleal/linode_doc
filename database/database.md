### Q：linode同一区域的Database与Linode之间是走内网还是外网？

A：外网，数据库与linode之间没有内网



###  Q: 数据库的ssl哪里关闭

A:  需要连接到数据库之后 进行更改 

```shell
	SET GLOBAL require_secure_transport=OFF;
	SET PERSIST require_secure_transport=OFF; 
```


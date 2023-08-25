### Q：Object Storage 能否进行service transfer 

 A：Object Storage不能进行service transfer，只能一个一个Object手动转入新的账号



### Q：哪些服务可以进行server transfer

 A：可以进行Service Transfer： Linode server、NodeBalancers

​	   不可以进行Service Transfer：Firewalls、DataBases、Object Storage



### Q：如何进行serverTransfer

A：在发出方创建一个serverTransfer

![image-20230714113253947](/Users/whalefalls/Desktop/project/book/picture/image-20230714113253947.png)

如果有未支付的账单 则无法进行serverTransfer

如果服务器有关联的firewalls 也是无法进行serverTransfer的
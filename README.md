# clover
clover

1、开发server和client端 定时向zk集群发送心跳数据包，利用Java自带的timer程序实现该功能 

2、开发整天的monitor程序，用来定时向zk中获取server和client端的心跳数据信息，如果超过指定时间没有收到最新的数据包，那么任务server端或者client端死掉了，此时要删除该server或client端节点，发邮件通知相关人员，记录异常日志到系统日志文件和MongoDB中 

3、client端接受创建job请求，将job信息创建到client服务端，并根据job时间规则运行，并将任务信息存储到MongoDB中 

4、当client端job运行时候，封装执行任务信息,发送到指定客户端机器，更新client端job执行时间和状态，如不在需要继续运行，那删除job并从MongoDB中删除相关任务信息 

5、client端接受删除job请求，client服务端，立即执行删除job并将任务信息从MongoDB中删除 

6、client端接受更新job请求，client服务端，立即执行删除job并创建新job,并将任务信息从MongoDB中删除,然后再存储新job信息 

7、第一版 使用Netty做消息通讯中间件，存储消息放入Redis中，服务器开启Http请求，客户端 通过 发送Http请求到服务器来处理请求，由于任务太多 redis处理能力不行，放弃该方案 第二版 使用Netty RPC框架，自己开发一个Server端和Client，各种启动指定端口，由于 必须要求Server端和Client必须启动才能进行消息发送，所以感觉非常不灵活，因为放弃该方案 第三版 使用架构组推荐的rocketmq,通过使用发现，很严重问题，消息会重复发送，经常会收到重复的消息，在测试的时候发现，经常发生消息异常和报错，跟架构组刘婷峰沟通说，可能是机器性能不行了，他也不知道具体原因，感觉非常不靠谱，果断放弃 第四版 使用 zeromq,通过在网上查资料，对比各种mq后，发现zeromq是最轻量级，出现消息是最快的，经过测试完全能满足业务，果断使用 

8、由于项目中使用zk,自己开发zk使用工具类，定制server端增删改查zk消息以及定制client端增删改查zk消息,功能测试zk,目前打算增加zk watch功能 

9、开发server和client端 定时向zk集群发送心跳数据包，利用Java自带的timer程序实现该功能 

10、开发整天的monitor程序，用来定时向zk中获取server和client端的心跳数据信息，如果超过指定时间没有收到最新的数据包，那么任务server端或者client端死掉了，此时要删除该server或client端节点，发邮件通知相关人员，记录异常日志到系统日志文件和MongoDB中 

11、开发console控制台管理，可以查看任务动态运行状态和次数信息 

12、zk管理页面，查看server和client端节点信息，更新和删除节点信息 

13、job管理页面，查看job详细信息 

14、联系人管理页面，增删改查联系人信息 

15、log日志管理页面，根据系统报错记录的日志信息，在页面中可以详细查看

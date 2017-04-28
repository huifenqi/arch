声明：目前的现状，我理解，是公司发展到目前状态的最好方式，后面列的都是公司未来希望快速，稳定，安全发展的个人看法，无任何对现状的抱怨，请知晓。

# 线上业务
## 安全、稳定
### 异常追踪系统
### 文件存储方式统一（一期）
当前使用状况：[http://123.57.69.21:9000/pages/viewpage.action?pageId=16714680][1]
目标：将所有文件存储和业务机器分离
问题：
1. 数据和服务混合，做高可用的前提是服务无状态，任意一台机器停了，有其他机器顶着，但数据混合着，没办法停机；
2. 文件下载请求过多，影响到了全站业务，。。。加带宽；DDOS，嗯，交保护费吧；
好处：解决如上问题

### 文件存储方式统一（二期）
目标：所有静态文件集中上云
问题：
1. 静态文件各自维护，成本高，全单点，做集群，维护成本更高；
	2. 无法抵御 DDOS;
	3. 无法对用户做加速；
	4.  资源利用率低。
好处：解决如上问题

### 文件存储方式统一（三期）
目标：文件分权限访问
问题：
1. 所有合同，个人身份证信息可被任何人下载；
2. 类似借贷宝的问题，借贷宝还是内部泄露的，我们是对公网开放的。
好处：解决如上问题  

### 高可用架构
目标：提升系统可用性
问题：
1. DDOS，业务中断；
2. 新功能部署，业务中断；
3. 机器出问题，业务中断。
好处：解决如上问题

### 入口收敛
目标：对外只有一个域名
问题：
1. 入口过多，针对 DDOS，需要多线解决。
好处：解决如上问题

### 公司内技术文化
目标：像个技术公司，金融公司
后面慢慢整理，大体包含 code review, 敏捷开发方式，技术分享，加强沟通，对外技术形象。

这些是一期内容，目前简单的计划了三期的，一些内容超出了作为架构师的职责，认可的前提下，你们请协助推动。

以上内容，可以给出你们的优先级，其中有不认可的，请指出。

=== 2017-04-12 update ===
Jmeter接口测试自动化: [http://www.cnblogs.com/111testing/p/6412173.html][2]
HTTP API自动化测试从手工到平台的演变： [http://www.infoq.com/cn/articles/http-api-automated-test-from-manual-to-platform][3]
jmeter 学习指南：[https://wuyan.gitbooks.io/jmeter/content/c1md.html][4]
Robot Framework ：[http://robotframework.org/][5]

[1]:	http://123.57.69.21:9000/pages/viewpage.action?pageId=16714680
[2]:	http://www.cnblogs.com/111testing/p/6412173.html
[3]:	http://www.infoq.com/cn/articles/http-api-automated-test-from-manual-to-platform
[4]:	https://wuyan.gitbooks.io/jmeter/content/c1md.html
[5]:	http://robotframework.org/
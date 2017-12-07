# architecture decision records

This repo records what decisions I made in the company.

Target: FinTech

1. Financial: Meet the financial compliance;
2. Technology: Make all tech related things follow the best practice and make them more automated.

Those all come from my short experience, so please read by your own risk.

1. [Record architecture decisions][1];
2. [团队中的密码管理][2];
3. [使用 ssh key 替换用户名密码方式登录][3];
4. [Ubuntu vs CentOS][4];
5. [使用 <del>BearyChat</del> Slack 替代微信、邮件和短信][5];
6. [使用 Git 替换 SVN][6];
7. [使用 PassPack 进行密码管理][7];
8. [使用堡垒机加强服务器安全][8];
9. [结构化 Django 项目][9];
10. [Git 基础及风格指南][10];
11. [Apply Github workflow to our team][11];
12. [Think about micro service][12];
13. [The sense of Done][13];
1. [Knowledge sharing][14];
16. [故障记录报告][15];
17. Incident classify and recovery;
18. [iOS 持续发布][16];
19. [服务器申请与升级 - 容量评估][17];
20. [日志管理][18];
21. [Redis 使用按业务分离并上云][19];
22. [防 DDOS 攻击][20];
23. [应用性能监控][21];
24. [实时错误跟踪][22];
25. [按 RESTful 风格设计更新服务接口][23];
26. [文件服务与业务服务隔离][24];
27. [消息队列][25];
28. What should we do when we setup a new server;
29. [本地 hosts 管理][26];
30. [容量评估 - 存储][27];
31. [容量评估 - 内存][28];
32. [TCP 长连接高可用][29];
33. [容量评估 - MySQL][30];
34. [DNS 笔记][31];
35. [关于灾难恢复][32];
36. [关于 MySQL 高可用][33];
37. [通过代理解决白名单问题][34];
38. [数据脱敏][35];
39. [秘钥管理][36];
40. [Agile - Daily standup meeting][37];
41. [MySQL 迁移 RDS 总结][38];
42. [Agile - Retrospective meeting][39];
43. [支持过滤的消息队列][40];
44. [泛域名解析][41]；
45. [Python 自建库的复用][42]；
40. code review;
41. Organize meetup as Company;
1. How to restart a server;
1. TBD.

[1]:	decisions/0001-record-architecture-decisions.md
[2]:	decisions/0002-manage-passwords-in-a-team.md
[3]:	decisions/0003-use-ssh-key-instead-of-password.md
[4]:	decisions/0004-replace-centos-with-ubuntu.md
[5]:	decisions/0005-replace-wechat-mail-sms-with-slack.md
[6]:	decisions/0006-replace-svn-with-git.md
[7]:	decisions/0007-use-passpack-to-manage-passwords.md
[8]:	decisions/0008-use-bastion-host-to-enhance-our-server-security.md
[9]:	decisions/0009-make-django-project-with-the-same-structure.md
[10]:	decisions/0010-git-basics-and-style-guide.md
[11]:	decisions/0011-apply-github-workflow-to-our-team.md
[12]:	decisions/0012-think-about-micro-service.md
[13]:	decisions/0013-the-sense-of-done.md
[14]:	decisions/0046-knowledge-sharing.md
[15]:	decisions/0016-post-mortem-report.md
[16]:	decisions/0018-continuous-delivery-ios.md
[17]:	decisions/0019-server-request-and-upgrade-capacity-evaluation.md
[18]:	decisions/0020-log-management.md
[19]:	decisions/0021-split-redis-with-business-and-move-redis-to-aliyun-kvstore.md
[20]:	decisions/0022-anti-ddos.md
[21]:	decisions/0023-application-performance-monitoring.md
[22]:	decisions/0024-exception-and-realtime-error-tracking.md
[23]:	decisions/0025-apply-restful-design-in-our-service-interface.md
[24]:	decisions/0026-move-files-to-independent-machine-and-aliyun-oss.md
[25]:	decisions/0027-message-queue.md
[26]:	decisions/0029-switch-hosts.md
[27]:	decisions/0030-capacity-evaluation-storage.md
[28]:	decisions/0031-capacity-evaluation-memory.md
[29]:	decisions/0032-ha-for-tcp-long-connection.md
[30]:	decisions/0033-capacity-evaluation-mysql.md
[31]:	decisions/0034-dns-notes.md
[32]:	decisions/0035-disaster-recovery.md
[33]:	decisions/0036-ha-for-mysql.md
[34]:	decisions/0037-use-proxy-for-white-list.md
[35]:	decisions/0038-data-masking.md
[36]:	decisions/0039-key-management.md
[37]:	decisions/0040-agile-daily-standup-meeting.md
[38]:	decisions/0041-the-summary-of-mysql-to-rds.md
[39]:	decisions/0042-agile-retrospective-meeting.md
[40]:	decisions/0043-message-queue-with-filter.md
[41]:	decisions/0044-wildcard-subdomain-resolution.md
[42]:	decisions/0045-reuse-python-custom-libs.md
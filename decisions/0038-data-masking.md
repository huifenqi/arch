# 38. 数据脱敏

Date: 2017-06-13

## Status

Accepted

## Context

1. 数据目前交由服务后台或前端进行敏感信息处理，原始数据存在多种风险（外部脱裤，内部人员非必要性的查看等）；
2. 各个 Team 数据加密策略不一致(有 MD5, AES etc)；
3. 数据掩码方式也不统一。

## Decision

使用四个策略的结合：

1. 掩码 - 业务系统需要查看部分内容，已核对信息，日志中为了便于定位；
2. 替换 - 字段实际不被使用，但保留字段，并将数据替换为空内容；
3. 可逆加密 - AES(ECB/PKCS5Padding - 128)
4. 不可逆加密 - SHA1

策略的使用需考虑，使用场景（生产、测试等环境），成本（对人员、服务器的需求），是否易用（影响开发效率），维度（目前就分两种：机密和公开）

掩码规则：

* 姓名 - `*斌` - 保留最后一个字，其余部分统一为一个星号
* 电话 - `131****0039` - 中间4\~7位每个字符替换为一个星号
* 身份证号 - `**************1234` - 保留后四位，其余部分每个字符替换为一个星号
* 银行卡号 - `3111111******1234` - 保留前六、后四位，其余部分每个字符替换为一个星号
* 地址 - \`\`
* 邮箱 - \`\`
* 密码 - \`\`
* 交易金额 - \`\`
* 充值码 - \`\`

两个原则：

1. remain meaningful for application logic(尽可能的为脱敏后的应用，保留脱敏前的有意义信息)
2. sufficiently treated to avoid reverse engineer(最大程度上防止黑客进行破解)

## Consequences

Refs:

* [动态数据脱敏最佳实践.pdf][1]
* 美团数据仓库-数据脱敏 [http://tech.meituan.com/data-mask.html][2]
* 大数据与数据脱敏 [https://zhuanlan.zhihu.com/p/20824603][3]
* 加解密详解 [http://www.jianshu.com/p/b3be35c1d424][4]
* 大数据隐私保护技术之脱敏技术探究 [http://www.freebuf.com/articles/database/120040.html][5]

[1]:	files/%E5%8A%A8%E6%80%81%E6%95%B0%E6%8D%AE%E8%84%B1%E6%95%8F%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.pdf
[2]:	http://tech.meituan.com/data-mask.html
[3]:	https://zhuanlan.zhihu.com/p/20824603
[4]:	http://www.jianshu.com/p/b3be35c1d424
[5]:	http://www.freebuf.com/articles/database/120040.html
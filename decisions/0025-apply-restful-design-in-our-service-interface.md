# 25. 按 RESTful 风格设计更新服务接口

Date: 04/05/2017

## Status

Accepted

## Context

1. 当前 URL 定义类似这样，`add_message`, `report_exception`, `check_pwd` 等，函数式定义，导致接口数量增长过快，管理麻烦；
2. 所有的请求都走 POST 方法；
3. 所有请求返回状态都是 200，使用晦涩难懂的自定义状态码；
4. 函数式编程，代码重用度不高；
5. 自定义接口文档，无法及时更新；
6. 返回结构差异化大，过滤，排序和分页各式各样，无统一的规范；
7. 无 API 控制台可供测试；
8. 更多。

## Decision

1. URL的设计应使用资源集合的概念；
	* 每种资源有两类网址（接口）：
		* 资源集合（例如，/orders）；
		* 集合中的单个资源（例如，/orders/{orderId}）。
	* 使用复数形式 (使用 ‘orders’ 而不是 ‘order’)；
	* 资源名称和 ID 组合可以作为一个网址的节点（例如，/orders/{orderId}/items/{itemId}）；
	* 尽可能的让网址越短越好，单个网址最好不超过三个节点。
2. 使用名词作为资源名称 (例如，不要在网址中使用动词)；
3. 使用有意义的资源描述；
	* “禁止单纯的使用 ID!” 响应信息中不应该存在单纯的 ID，应使用链接或是引用的对象；
	* 设计资源的描述信息，而不是简简单单的做数据库表的映射；
	* 合并描述信息，不要通过两个 ID 直接表示两个表的关系；
4. 资源的集合应支持过滤，排序和分页；
5. 支持通过链接扩展关系，允许客户端通过添加链接扩展响应中的数据；
6. 支持资源的字段裁剪，运行客户端减少响应中返回的字段数量；
7. 使用 HTTP 方法名来表示对应的行为：
	* POST - 创建资源，非幂等性操作；
	* PUT - 更新资源（替换）；
	* PATCH - 更新资源（部分更新）；
	* GET - 获取单个资源或资源集合；
	* DELETE - 删除单个资源或资源集合；
8. 合理使用 HTTP 状态码；
	* 200 - 成功；
	* 201 - 创建成功，成功创建一个新资源时返回。 返回信息中将包含一个 'Location' 报头，他通过一个链接指向新创建的资源地址；
	* 400 - 错误的请求，数据问题，如不正确的 JSON 等；
	* 404 - 未找到，通过 GET 请求未找到对应的资源；
	* 409 - 冲突，将出现重复的数据或是无效的数据状态。
9. 使用 ISO 8601 时间戳格式来表示日期；
10. 确保你的 GET，PUT，DELETE 请求是[幂等的][1]，这些请求多次操作不应该有副作用。
11. PUT、POST、PATCH 请求参数通过 `application/json` 传递；
12. 正确返回格式：
	* 单个资源：{field1: value1, …}
	* 资源集合：[{field1: value1, …}]
	* 资源集合（带分页）：
```json
{
 "count": 0,
 "next": null,
 "previous": null,
 "results": [{"field1": "value1", …}]
}
```
13. 错误返回格式：
	* 非特定字段错误
```json 
{
 "non_field_errors": [
  "该手机号码未注册！"
 ]
}
```
* 特定字段错误
```json
{
 "phone_number": [
  "该字段不能为空。"
 ],
 "address": [
  "该字段不能为空。"
 ]
}
```
14.  使用  swagger  做 API 展示 与调试。
	![][image-1]

## Consequences

Refs:

* API 设计参考手册 [https://github.com/iamsk/api-cheat-sheet/blob/master/README-zh-Hans.md][2]
* Best Practices for Designing a Pragmatic RESTful API [http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api][3]
* REST API Quick Tips [http://www.restapitutorial.com/lessons/restquicktips.html][4]
* Django REST framework [http://www.django-rest-framework.org/][5]

[1]:	http://www.restapitutorial.com/lessons/idempotency.html
[2]:	https://github.com/iamsk/api-cheat-sheet/blob/master/README-zh-Hans.md
[3]:	http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api
[4]:	http://www.restapitutorial.com/lessons/restquicktips.html
[5]:	http://www.django-rest-framework.org/

[image-1]:	files/swagger.png
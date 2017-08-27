# 39. 秘钥管理

Date: 2017-06-14

## Status

Accepted

## Context

1. 目前有相当多的账户、密码等信息存储在项目配置文件中；
2. 部分项目将敏感信息和项目分离，但所部署的服务器还是能被所有人登录查看；
3. 将服务器登录权限限制在运维手中，需要运维人员维护所有敏感信息的存储与管理，数量线性增长，尤其是支付组涉及的敏感信息更多，每一个新项目都需要运维人员的参与和维护。

## Decision

1. 将服务器登录权限限制在个别人的手中；
2. 使用密码管理服务，确保运维人员只需维护一个秘钥；
3. 使用 Aliyun KMS 而不是自己搭建，节约运维成本。

直接使用KMS加密、解密

![][image-1]

结合我们的需求，我们选用这种方式，使用方式如下

```python
import json
from aliyunsdkcore.client import AcsClient
from aliyunsdkkms.request.v20160120 import EncryptRequest, DecryptRequest

OLD = 'password'
NEW = 'M2U5YzZlNGEtZTczZS00NmM4LWE0YmQtZjI3ODI0MmU4YWJjcEVDZW5SMEtWYjJsdWovdU5ibFNhSk5KS0RqbE9ENTRBQUFBQUFBQUFBQXJOd2dGc2l4S1JpV0tPRUgvbkwvSXVHYU5heCt5eHlFPQ=='

client = AcsClient('id', 'secret', 'cn-beijing')


def en():
    request = EncryptRequest.EncryptRequest()
    request.set_KeyId('e6116a43-9926-4a66-a781-55fce623c2cb')
    request.set_Plaintext(OLD)
    response = client.do_action_with_exception(request)
    print json.loads(response)['CiphertextBlob']


def de():
    request = DecryptRequest.DecryptRequest()
    request.set_CiphertextBlob(NEW)
    response = client.do_action_with_exception(request)
    print json.loads(response)['Plaintext'] == OLD


if __name__ == '__main__':
    de()
```

使用信封加密在本地加密、解密

![][image-2]

![][image-3]

## Consequences

1. 直接使用KMS加密、解密会影响启动速度；
2. 一个明文多次加密，产生的密文不同，但所有密文都可以解密为明文。

Refs:

* 使用场景 [https://help.aliyun.com/document\_detail/28937.html][1]
* 什么是信封加密？[https://help.aliyun.com/knowledge\_detail/42339.html][2]
* Python SDK使用说明 [https://help.aliyun.com/document\_detail/53090.html][3]
* KMS SDK source: [https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-kms/aliyunsdkkms/request/v20160120][4]
* 结合KMS实现本地文件加解密 [https://help.aliyun.com/video\_detail/54134.html][5]
* JAVA SDK样例代码 [https://help.aliyun.com/document\_detail/43347.html][6]

[1]:	https://help.aliyun.com/document_detail/28937.html
[2]:	https://help.aliyun.com/knowledge_detail/42339.html
[3]:	https://help.aliyun.com/document_detail/53090.html
[4]:	https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-kms/aliyunsdkkms/request/v20160120
[5]:	https://help.aliyun.com/video_detail/54134.html
[6]:	https://help.aliyun.com/document_detail/43347.html

[image-1]:	files/kms-scenario1.png
[image-2]:	files/kms-scenario2.1.png
[image-3]:	files/kms-scenario2.2.png
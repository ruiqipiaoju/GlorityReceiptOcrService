# GlorityReceiptOcrService
睿琪票据  https://fapiao.glority.cn

## 发票识别

### 调用地址

https://fapiao.glority.cn/v1/item/get_item_info

### 请求方式

GET/POST

### 返回类型

JSON

### 请求参数

| 名称 | 变量名 | 必填 | 类型 | 示例值| 描述 |
| --- | -----  | ---- | --- | ----- | --- |
| Key | app_key | true | String(32) | c5ed72329fece2fe0010a437505b01cb | 分配的key  
| 令牌 | token | true | String(32) | 7007bd1257dce8d47489166a7c77a926 | 授权令牌  
| 时间戳 | timestamp | true | String(32) | 1522374165 | timestamp 为January 1 1970 00:00:00 GMT 到现在的秒数  
| 图片链接 | image_url | false | String | http://fapiao.glority.cn/dist/img/sample.jpg | 图片链接地址  
| 图片文件 | image_file | false | Binary |  | 图片文件  
| 图片Base64数据 | image_data | false | String |  | 图片Base64数据  
| 识别类型 | type | false | int | 0 | 要识别的发票类型:<br>0: 自动识别(默认值)<br>1: 增值税发票(大票)<br>2: 出租车,火车票, 机打发票, 增值税卷票(小票-自动识别) |

### 说明
- 支持的图片类型: jpg, jpeg, png及pdf(pdf只支持识别第一页内容). 图片最大支持8M. 
  - 建议分辨率过大的可以进行压缩(查看压缩示例代码)
- token 的值计算方式为：md5($appkey+$timestamp+$appSecret) 
  - token=md5("c5ed72329fece2fe0010a437505b01cb+1522374165+5c9597f3c8245907ea71a89d9d39d08e")=7007bd1257dce8d47489166a7c77a926
- API请求示例： 
  - https://fapiao.glority.cn/v1/item/get_item_info?app_key=c5ed72329fece2fe0010a437505b01cb&timestamp=1522374165&token=7007bd1257dce8d47489166a7c77a926&image_url=http://fapiao.glority.cn/dist/img/sample.jpg
- 生成token时，字符串连接中的“+”是必需的，缺少这个符号会无法验证通过验证

## 多张发票信息识别

### 调用地址

https://fapiao.glority.cn/v1/item/get_multiple_items_info

### 请求方式

GET/POST

### 返回类型

JSON

### 请求参数

| 名称 | 变量名 | 必填 | 类型 | 示例值| 描述 |
| --- | -----  | ---- | --- | ----- | --- |
| Key | app_key | true | String(32) | c5ed72329fece2fe0010a437505b01cb | 分配的key  
| 令牌 | token | true | String(32) | 7007bd1257dce8d47489166a7c77a926 | 授权令牌  
| 时间戳 | timestamp | true | String(32) | 1522374165 | timestamp 为January 1 1970 00:00:00 GMT 到现在的秒数  
| 图片链接 | image_url | false | String | http://fapiao.glority.cn/dist/img/sample.jpg | 图片链接地址  
| 图片文件 | image_file | false | Binary |  | 图片文件  
| 图片Base64数据 | image_data | false | String |  | 图片Base64数据  

### 说明
- 支持的图片类型: jpg, jpeg, png及pdf(pdf只支持识别第一页内容). 图片最大支持8M. 
  - 建议分辨率过大的可以进行压缩(查看压缩示例代码)
- token 的值计算方式为：md5($appkey+$timestamp+$appSecret) 
  - token=md5("c5ed72329fece2fe0010a437505b01cb+1522374165+5c9597f3c8245907ea71a89d9d39d08e")=7007bd1257dce8d47489166a7c77a926
- API请求示例： 
  - https://fapiao.glority.cn/v1/item/get_multiple_items_info?app_key=c5ed72329fece2fe0010a437505b01cb&timestamp=1522374165&token=7007bd1257dce8d47489166a7c77a926&image_url=http://fapiao.glority.cn/dist/img/sample.jpg
- 生成token时，字符串连接中的“+”是必需的，缺少这个符号会无法验证通过验证


## 发票信息识别结果反馈

### 调用地址

https://fapiao.glority.cn/v1/item/feedback

### 请求方式

GET/POST

### 返回类型

JSON

### 请求参数

| 名称 | 变量名 | 必填 | 类型 | 示例值| 描述 |
| --- | -----  | ---- | --- | ----- | --- |
| Key | app_key | true | String(32) | c5ed72329fece2fe0010a437505b01cb | 分配的key  
| 令牌 | token | true | String(32) | 7007bd1257dce8d47489166a7c77a926 | 授权令牌  
| 时间戳 | timestamp | true | String(32) | 1522374165 | timestamp 为January 1 1970 00:00:00 GMT 到现在的秒数  
| 图片链接 | image_url | false | String | http://fapiao.glority.cn/dist/img/sample.jpg | 图片链接地址  
| 图片文件 | image_file | false | Binary |  | 图片文件  
| 图片Base64数据 | image_data | false | String |  | 图片Base64数据  
| 识别结果 | result	 | false | int | 0或者1	 | 	0：识别结果有错误(默认值) <br>1：识别结果正确<br>如果这个参数不传，默认为0 |

### 说明
- 支持两种方式反馈发票信息识别结果

  1.使用识别结果中的标识id（输入参数中的 id）

  2.上传图片文件 （输入参数中的 image_url, image_file 和image_data 中的一个）

- 注意事项：

  1.如果使用标识id返回结果，即代表同意上传识别的发票在服务器上缓存一段时间,请预先联系我们，需要对账号进行相应设置.

## 公共说明

### 正确返回参数

| 名称 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 返回状态码 | result | true | int | 0或1 | 请求状态. 1:成功, 0:失败 |
| 回复 | response | true | json  |  |   |

### 失败返回参数

| 名称 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 返回状态码 | result | true | int | 0或1 | 请求状态. 1:成功, 0:失败 |
| 错误码 | error | true | int | 10002 |  |
| 信息说明  | message  | true  | String  | "Autdenticate failed" |  |

### 失败返回样例

```
{
    'result': 0,
    'error': 10002,
    'message': 'Authenticate failed'
}
```

### 错误码定义

| 名称 | 描述 | 原因 | 解决方案 |
| --- | --- | --- | ---|
| 10000 | Internal error | 服务器内部错误 | 请联系管理员 |
| 10002 | Authenticate failed | 授权错误 | 请确认已使用有效的appkey以及appsecret获取token，获取方法上文已述 |
| 10003 | Invalid parameter | 无效参数 | 补充相关必要参数 |
| 10004 | Not support type | 不支持的发票类型 | 该种类型发票尚不支持 |
| 10005 | Invalid type | 发票类型不对 | 1, 识别的发票类型 与 输入的“type”不一致, 检查输入的参数与要识别的图片. 2, 当前账号没有识别该类型发票的权限. 购买相应权限或者联系管理员. |
| 10006 | Invalid image | 无效图片 | 请检查以下几点: 1, 是否是损坏的图片 2, 是否是不支持的图片格式 3, 是否图片大小超过限制 |
| 10007 | No available packet | 无可用的流量包 | 购买新流量包或联系管理员 |
| 10008 | Image cache disabled | 图片缓存功能未开启 | 调用/feedback api时使用了id字段，但是图片缓存功能未开启，请联系管理员 |
| 10025 | Invalid app key | 无效App Key | 检查appkey，确保有效 |
| 10026 | Expired token | token过期 | 重新生成token |
| 10300 | pdf convert failed | pdf文件处理异常 | 请联系管理员 |
| 10400 | download image file failed | 使用image_url参数时图片下载失败 | 1.检查图片url是否正确 <br>2.检查图片能否正常下载,图片下载timeout为20秒 |

### 发票类型

| 名称 | 描述 | 名称 | 描述 | 名称 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 10100 | 增值税专用发票 | 10200 | 定额发票 | 10507 | 过路费发票 |
| 10101 | 增值税普通发票 | 10400 | 机打发票 | 10900 | 可报销其他发票 |
| 10102 | 增值税电子普通发票 | 10500 | 出租车发票 | 00000 | 其他 |
| 10103 | 增值税普通发票(卷票) | 10503 | 火车票 | 20100 | 国际小票 |
| 10104 | 机动车销售统一发票 | 10505 | 客运汽车 |  |  |
| 10105 | 二手车销售统一发票 | 10506 | 航空运输电子客票行程单 |  |  |

### 消费类型

| Food&amp;Dining | Transport | Shopping | Bills | Other |
| --- | --- | --- | --- | --- |
| Lodging | Travel | Car | Services |  |
| Health_Fitness | Education | Shipping | Equipment |  |

# FakeXiecheng API接口文档

本文档列出了FakeXiecheng API的部分路由和它们的请求和响应。 FakeXiecheng API提供了虚拟的旅游路线信息，可以通过HTTP接口获取数据。

## 公共请求头

以下是所有路由共用的请求头：

| 名称            | 类型     | 是否必需 | 说明                       |
| ------------- | ------ | ---- | ------------------------ |
| Authorization | string | 是    | 使用Bearer token方式认证API调用。 |





# 接口说明

以下接口的详细说明：

1. GET /api/touristRoutes

- 描述：获取所有旅游路线列表
- 请求参数：无
- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)
- 响应体：旅游路线列表（JSON数组）
- 响应状态：200 OK

1. GET /api/touristRoutes/{touristRouteId}

- 描述：获取指定ID的旅游路线详情
- 请求参数：touristRouteId（string，路线ID）
- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)
- 响应体：旅游路线详情（JSON对象）
- 响应状态：200 OK

1. POST /api/touristRoutes

- 描述：创建一条新的旅游路线
- 请求参数：旅游路线信息（JSON对象）
- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)
- 响应体：新创建的旅游路线ID
- 响应状态：201 Created

1. PUT /api/touristRoutes/{touristRouteId}

- 描述：更新指定ID的旅游路线信息
- 请求参数：旅游路线信息（JSON对象）
- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)
- 响应体：无
- 响应状态：204 No Content

1. PATCH /api/touristRoutes/{touristRouteId}

- 描述：更新指定ID的旅游路线部分信息
- 请求参数：旅游路线信息的JSON Patch（JSON数组）
- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)
- 响应体：无
- 响应状态：204 No Content

1. DELETE /api/touristRoutes/{touristRouteId}

- 描述：删除指定ID的旅游路线

- 请求参数：touristRouteId（string，路线ID）

- 请求头：Authorization: Bearer [access_token] (必须，JWT认证)

- 响应体：无

- 响应状态：204 No Content

  ​

## 用户登录认证

### 请求信息

- 请求路径：<http://106.14.174.76:8080/auth/login>
- 请求方法：POST

### 请求参数

| 参数名      | 参数类型   | 是否必填 | 参数说明 |
| -------- | ------ | ---- | ---- |
| email    | string | 是    | 用户邮箱 |
| password | string | 是    | 用户密码 |

### 请求头部

无

### 响应信息

### 响应体

成功登录后，将返回一个JWT Token。Token应被存储并在接下来的所有请求中包含在Authorization头部中。

### 响应头部

无

### 响应示例

```
Copy code
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5MDE4NDE1NS1kZWUwLTQwYzktYmIxZS1iNWVkMDdhZm
```





## 注册用户

### 请求

`POST http://106.14.174.76:8080/auth/register`

### 请求参数

| 参数名             | 类型     | 是否必填 | 说明     |
| --------------- | ------ | ---- | ------ |
| email           | string | 是    | 用户邮箱地址 |
| password        | string | 是    | 用户密码   |
| confirmPassword | string | 是    | 确认密码   |

### 请求示例

```
jsonCopy code
{
    "email": "alex1234@163.com",
    "password": "Fake123$",
    "confirmPassword": "Fake123$"
}

```

### 响应

#### 响应体

当请求参数有误时：

```
jsonCopy code
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "Bad Request",
    "status": 400,
    "traceId": "|de24eb77-473eccbe8095a8c7."
}

```

#### 响应头部

无特殊要求。

### 响应示例

当请求参数有误时：

```
jsonCopy code
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
    "title": "Bad Request",
    "status": 400,
    "traceId": "|de24eb77-473eccbe8095a8c7."
}
```





## 获取旅游路线列表

获取所有旅游路线的列表信息。

- 请求路径：`http://106.14.174.76:8080/api/touristRoutes`
- 请求方法：`GET`

### 请求头部

| 参数            | 参数值                   | 是否必须 | 说明                         |
| ------------- | --------------------- | ---- | -------------------------- |
| Authorization | Bearer [access_token] | 是    | 授权信息，access_token需通过登录接口获取 |

### 请求参数

该接口无需传入请求参数。

### 响应内容

返回所有旅游路线的列表信息。

| 参数              | 类型     | 说明        |
| --------------- | ------ | --------- |
| id              | string | 旅游路线的ID   |
| title           | string | 旅游路线的标题   |
| description     | string | 旅游路线的描述   |
| price           | number | 旅游路线的价格   |
| originalPrice   | number | 旅游路线的原价   |
| discountPresent | number | 旅游路线的折扣   |
| rating          | number | 旅游路线的评分   |
| travelDays      | string | 旅游路线的天数   |
| tripType        | string | 旅游路线的类型   |
| departureCity   | string | 旅游路线的出发城市 |
| createTime      | string | 旅游路线的创建时间 |
| updateTime      | string | 旅游路线的更新时间 |
| departureTime   | string | 旅游路线的出发时间 |
| features        | string | 旅游路线的特色   |

### 响应头部

该接口无需返回响应头部信息。





## 获取旅游路线信息

获取指定id的旅游路线信息。

### 请求

`GET /api/touristRoutes/{id}`

### 请求参数

| 参数   | 类型     | 描述         |
| ---- | ------ | ---------- |
| id   | string | 旅游路线的唯一标识符 |

### 请求头

| 参数            | 类型     | 描述                           |
| ------------- | ------ | ---------------------------- |
| Authorization | string | 用于验证请求的身份，Bearer + 授权Token组成 |

### 响应

| 参数              | 类型     | 描述         |
| --------------- | ------ | ---------- |
| id              | string | 旅游路线的唯一标识符 |
| title           | string | 旅游路线的标题    |
| description     | string | 旅游路线的描述    |
| price           | float  | 旅游路线的价格    |
| originalPrice   | float  | 旅游路线的原始价格  |
| discountPresent | float  | 折扣百分比      |
| rating          | float  | 旅游路线的评分    |
| travelDays      | string | 旅游路线的天数    |
| tripType        | string | 旅游路线的类型    |
| departureCity   | string | 出发城市       |
| createTime      | string | 旅游路线的创建时间  |
| updateTime      | string | 旅游路线的更新时间  |
| departureTime   | string | 出发时间       |
| features        | string | 旅游路线的特色项目  |

### 响应示例

```
swiftCopy code
{
    "id": "39996f34-013c-4fc6-b1b3-0c1036c47110",
    "title": "摩洛哥撒哈拉沙漠+卡萨布兰卡+马拉喀什+舍夫沙万12日跟团游(4钻)",
    "description": "【世界加油】明星一价全包|免签|25人封顶|特色沙漠酒店夜观繁星+卡萨升国5喜来登|赠骆驼骑行换装秀+撒哈拉四驱车+YSL花园下午茶+表演秀|网红餐厅",
    "price": 15490.00,
    "originalPrice": 15490.00,
    "discountPresent": null,
    "rating": 3.2,
    "travelDays": "Three",
    "tripType": "BackPackTour",
    "departureCity": "Shenzhen",
    "createTime": "0001-01-01T00:00:00",
    "updateTime": null,
    "departureTime": null,
    "features": "<div class=\"bd\"><p style=\"text-align:center\"><strong><span style=
```





## 获取旅游路线图片信息

- 接口路径：`http://106.14.174.76:8080/api/touristRoutes/{touristRouteId}/pictures/{pictureId}`
- 请求方式：GET

### 请求头

| 参数名           | 参数值                                      |
| ------------- | ---------------------------------------- |
| Authorization | Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9... (用户token) |

### 请求参数

| 参数名            | 参数类型   | 是否必填 | 描述   |
| -------------- | ------ | ---- | ---- |
| touristRouteId | string | 是    | 路线ID |
| pictureId      | int    | 是    | 图片ID |

### 响应参数

| 参数名            | 参数类型   | 是否必填 | 描述     |
| -------------- | ------ | ---- | ------ |
| id             | int    | 是    | 图片ID   |
| url            | string | 是    | 图片地址   |
| touristRouteId | string | 是    | 旅游路线ID |

### 响应示例

```
jsonCopy code
{
    "id": 1,
    "url": "../../assets/images/louvre-102840_640.jpg",
    "touristRouteId": "fb6d4f10-79ed-4aff-a915-4ce29dc9c7e1"
}

```

### 响应状态码

| 状态码  | 描述   |
| ---- | ---- |
| 200  | 请求成功 |
| 401  | 未授权  |
| 404  | 未找到  |



## 获取旅游路线图片列表

### 请求

- 接口路径：`http://106.14.174.76:8080/api/touristRoutes/{touristRouteId}/pictures`

- 请求方式：`GET`

- 请求参数：

  | 参数名            | 类型     | 是否必须 | 描述          |
  | -------------- | ------ | ---- | ----------- |
  | touristRouteId | string | 是    | 旅游路线id      |
  | page           | int    | 否    | 分页页码，默认为1   |
  | size           | int    | 否    | 分页每页大小，默认为5 |

- 请求头：

  | 参数名           | 类型     | 是否必须 | 描述                          |
  | ------------- | ------ | ---- | --------------------------- |
  | Authorization | string | 是    | 用户token，格式为`Bearer {token}` |

### 响应

- 响应状态码：200 OK

- 响应参数：

  | 参数名            | 类型     | 是否必须 | 描述     |
  | -------------- | ------ | ---- | ------ |
  | id             | int    | 是    | 图片id   |
  | url            | string | 是    | 图片url  |
  | touristRouteId | string | 是    | 旅游路线id |

- 响应示例：

  ```
  cssCopy code
  [    {        "id": 28,        "url": "../../assets/images/louvre-102840_640.jpg",        "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"    },    {        "id": 29,        "url": "../../assets/images/louvre-102840_640.jpg",        "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"    },    {        "id": 30,        "url": "../../assets/images/louvre-102840_640.jpg",        "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"    },    {        "id": 31,        "url": "../../assets/images/louvre-102840_640.jpg",        "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"    }]

  ```

### 错误响应

- 响应状态码：401 Unauthorized

- 响应示例：

  ```
  jsonCopy code
  {
      "type": "https://tools.ietf.org/html/rfc7235#section-3.1",
      "title": "Unauthorized",
      "status": 401,
      "traceId": "|ccc8e546-4a55a0a31bbf5b9c."
  }

  ```

- 响应状态码：404 Not Found

- 响应示例：

  ```
  jsonCopy code
  {
      "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
      "title": "Not Found",
      "status": 404,
      "traceId": "|ccc8e54-4a55a0a31bbf5b9c."
  }
  ```



## 创建旅游路线

- 接口描述：创建一条新的旅游路线

- 请求URL：`http://106.14.174.76:8080/api/touristRoutes`

- 请求方式：POST

- 请求头：

  - Authorization: Bearer [access_token] (必须，JWT认证)

- 请求体：

  ```
  jsonCopy code
  {
      "title": "hello test222",
      "description": "hello test hello test hello test hello test hello test hello test hello test",
      "price": 0.0,
      "originalPrice": 0.0,
      "discountPresent": null,
      "rating": null,
      "travelDays": "",
      "tripType": "",
      "departureCity": "",
      "departureTime": null,
      "features": null,
      "fees": null,
      "notes": null
  }

  ```

- 响应体：

  ```
  jsonCopy code
  {
      "id": "891455e4-0206-4729-9886-db81c4a867e7",
      "title": "hello test222",
      "description": "hello test hello test hello test hello test hello test hello test hello test",
      "price": 0.0,
      "originalPrice": 0.0,
      "discountPresent": null,
      "rating": null,
      "travelDays": "",
      "tripType": "",
      "departureCity": "",
      "createTime": "0001-01-01T00:00:00",
      "updateTime": null,
      "departureTime": null,
      "features": null,
      "fees": null,
      "notes": null,
      "touristRoutePictures": [],
      "links": [
          {
              "href": "http://106.14.174.76:8080/api/TouristRoutes/891455e4-0206-4729-9886-db81c4a867e7",
              "rel": "self",
              "method": "GET"
          },
          {
              "href": "http://106.14.174.76:8080/api/TouristRoutes/891455e4-0206-4729-9886-db81c4a867e7",
              "rel": "update",
              "method": "PUT"
          },
          {
              "href": "http://106.14.174.76:8080/api/TouristRoutes/891455e4-0206-4729-9886-db81c4a867e7",
              "rel": "partially_update",
              "method": "PATCH"
          },
          {
              "href": "http://106.14.174.76:8080/api/TouristRoutes/891455e4-0206-4729-9886-db81c4a867e7",
              "rel": "delete",
              "method": "DELETE"
          },
          {
              "href": "http://106.14.174.76:8080/api/touristRoutes/891455e4-0206-4729-9886-db81c4a867e7/pictures",
              "rel": "get_pictures",
              "method": "GET"
          },
          {
              "href": "http://106.14.174.76:8080/api/touristRoutes/891455e4-0206-4729-9886-db81c4a867e7/pictures",
              "rel": "create_picture",
             
  ```



## 创建旅游路线(带图片)

- 接口说明：创建新的旅游路线
- 请求路径：`http://106.14.174.76:8080/api/touristRoutes`
- 请求方法：POST
- 请求参数：

| 参数名                  | 类型     | 是否必填 | 描述                  |
| -------------------- | ------ | ---- | ------------------- |
| title                | string | 是    | 旅游路线标题              |
| description          | string | 是    | 旅游路线描述              |
| originalPrice        | float  | 是    | 旅游路线原价              |
| discountPercent      | float  | 否    | 旅游路线折扣（范围为0-1之间的小数） |
| touristRoutePictures | array  | 否    | 旅游路线图片              |

其中，touristRoutePictures为数组，每个元素如下：

| 参数名  | 类型     | 是否必填 | 描述        |
| ---- | ------ | ---- | --------- |
| url  | string | 是    | 旅游路线图片url |

- 请求头：

| 参数名           | 类型     | 是否必填 | 描述                 |
| ------------- | ------ | ---- | ------------------ |
| Authorization | string | 是    | 访问令牌（Bearer token） |

- 响应体：

| 参数名                  | 类型       | 描述                                    |
| -------------------- | -------- | ------------------------------------- |
| id                   | string   | 旅游路线id                                |
| title                | string   | 旅游路线标题                                |
| description          | string   | 旅游路线描述                                |
| price                | float    | 旅游路线现价（原价 * 折扣百分比）                    |
| originalPrice        | float    | 旅游路线原价                                |
| discountPresent      | float    | 旅游路线折扣百分比                             |
| rating               | float    | 旅游路线评分                                |
| travelDays           | string   | 旅游路线行程天数                              |
| tripType             | string   | 旅游路线类型                                |
| departureCity        | string   | 旅游路线出发城市                              |
| createTime           | datetime | 旅游路线创建时间                              |
| updateTime           | datetime | 旅游路线更新时间                              |
| departureTime        | datetime | 旅游路线出发时间                              |
| features             | string   | 旅游路线特色（以逗号分隔的字符串）                     |
| fees                 | string   | 旅游路线费用（以逗号分隔的字符串）                     |
| notes                | string   | 旅游路线预定须知（以逗号分隔的字符串）                   |
| touristRoutePictures | array    | 旅游路线图片数组，每个元素如下：id、url、touristRouteId |
| links                | array    | 该资源相关的链接，每个元素如下：href、rel、method       |

响应示例：

```
{
    "id": "a4c4754f-0ea5-4538-8270-0496179fc5ee",
    "title": "hello test222",
    "description": "hello test hello test hello test hello test hello test hello test hello test",
    "price": 0.0,
    "originalPrice": 0.0,
    "discountPresent": null,
    "rating": null,
    "travelDays": "",
    "tripType": "",
    "departureCity": "",
    "createTime": "0001-01-01T00:00:00",
    "updateTime": null,
    "departureTime": null,
    "features": null,
    "fees": null,
    "notes": null,
    "touristRoutePictures": [
        {
            "id": 69,
            "url": "../../assets/images/osaka-castle-1398116_640.jpg",
            "touristRouteId": "a4c4754f-0ea5-4538-8270-0496179fc5ee"
        },
        {
            "id": 70,
            "url": "../../assets/images/22222222.jpg",
            "touristRouteId": "a4c4754f-0ea5-4538-8270-0496179fc5ee"
        }
    ],
    "links": [
        {
            "href": "http://106.14.174.76:8080/api/TouristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "http://106.14.174.76:8080/api/TouristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee",
            "rel": "update",
            "method": "PUT"
        },
        {
            "href": "http://106.14.174.76:8080/api/TouristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee",
            "rel": "partially_update",
            "method": "PATCH"
        },
        {
            "href": "http://106.14.174.76:8080/api/TouristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee",
            "rel": "delete",
            "method": "DELETE"
        },
        {
            "href": "http://106.14.174.76:8080/api/touristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee/pictures",
            "rel": "get_pictures",
            "method": "GET"
        },
        {
            "href": "http://106.14.174.76:8080/api/touristRoutes/a4c4754f-0ea5-4538-8270-0496179fc5ee/pictures",
            "rel": "create_picture",
            "method": "POST"
        }
    ]
}
```





## 根据ID全部更新旅游路线信息。

### 请求URL

- `PUT` <http://106.14.174.76:8080/api/touristRoutes/39996f34-013c-4fc6-b1b3-0c1036c47110>

### 请求参数

| 参数名                  | 必选   | 类型     | 说明                                       |
| -------------------- | ---- | ------ | ---------------------------------------- |
| title                | 是    | string | 旅游路线标题                                   |
| description          | 是    | string | 旅游路线描述                                   |
| price                | 是    | float  | 旅游路线价格                                   |
| createTime           | 是    | string | 旅游路线创建时间（格式：yyyy-MM-ddTHH:mm:ss）         |
| updateTime           | 否    | string | 旅游路线更新时间（格式：yyyy-MM-ddTHH:mm:ss），如果不修改传null |
| departureTime        | 否    | string | 旅游路线出发时间（格式：yyyy-MM-ddTHH:mm:ss），如果不修改传null |
| features             | 是    | string | 旅游路线特色                                   |
| rating               | 是    | float  | 旅游路线评分（最高5分）                             |
| travelDays           | 是    | string | 旅游路线天数                                   |
| tripType             | 是    | string | 旅游路线类型（枚举值：SelfGuidedTour，GroupTour，BackPackTour） |
| departureCity        | 是    | string | 旅游路线出发城市                                 |
| touristRoutePictures | 是    | array  | 旅游路线图片列表                                 |
| id                   | 是    | int    | 旅游路线图片ID                                 |
| url                  | 是    | string | 旅游路线图片URL                                |
| touristRouteId       | 是    | string | 旅游路线ID                                   |

### 请求示例

```
swiftCopy code
PUT http://106.14.174.76:8080/api/touristRoutes/39996f34-013c-4fc6-b1b3-0c1036c47110

{
    "title": "hello update11",
    "description": "【世界加油】明星一价全包|免签|25人封顶|特色沙漠酒店夜观繁星+卡萨升国5喜来登|赠骆驼骑行换装秀+撒哈拉四驱车+YSL花园下午茶+表演秀|网红餐厅1",
    "price": 15440.00,
    "createTime": "0001-01-01T00:00:00",
    "updateTime": null,
    "departureTime": null,
    "features": "<div class=\"bd\"><p style=\"text-align:center\"><strong><span style=\"color:#ffffff;font-size:24px\"><a href=\"http://vacations.ctrip.com/tour/detail/p19441039s2.html\" target=\"_blank\"></a></span></strong><strong style=\"color:rgb(192, 0, 0)\"><span style=\"font-size:24px\">【2020自营一价包升级款：埃及五星尼罗河游轮+红海度假+古文明探索12日内陆飞机精品团】</span></strong></p><p style=\"text-align:center\"><span style=\"color:rgb(192, 0, 0)\"><strong><span style=\"color:rgb(192, 0, 0);font-size:14px\"><strong style=\"color:rgb(34, 34, 34);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;font-size:14px;text-align:center;white-space:normal;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);font-size:24px;position:static;height:auto\">【25人封顶小团|增加底比斯古都停留|赠特色项目|行程更舒适】</span></strong></span></strong></span></p><p style=\"text-align:center\"><span style=\"color:rgb(0, 0, 0)\"><span style=\"font-size:14px;background-color:rgb(255, 255, 255)\">*畅销好评多年,超6000人出游超好评</span><span style=\"font-size:14px;background-color:rgb(255, 255, 255)\">！线路可以模仿,品质无法同比,图片可以抄袭,点评无法仿造*</span></span><br></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);text-align:center;font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><br></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【升级说明】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">2020年明星产品再次升级，一生只去一次的埃及不能只看表面，食住行游娱之外更重要的就是中文导游专业讲解，我们多年合作的优质中文导游队伍一定让您不虚此行！</span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><strong style=\"float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">冬季重磅升级·跟团游玩出新花样</span></strong></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【人数封顶】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">整团人数25位封顶，告别拥挤超级大团！</span></span><span style=\"color:rgb(192, 0, 0);position:static;height:auto\"><br>☆【住卢克索】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">卢克索尼罗河畔住宿1晚，底比斯古都私属时光！</span></span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【超长游览】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">埃及历史博物馆超长游览3小时,不留遗憾！</span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【特色项目】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">乘马车晨游底比斯古都，你会懂为什么那么多电影大片偏爱卢克索！</span></span><span style=\"color:rgb(192, 0, 0);position:static;height:auto\"><br>☆【特别安排】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">学画象形文字，制作一幅属于自己的纸草画！（每人赠送1张）</span></span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【巴士升级】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">16位游客以上团队直接升级奔驰品牌巴士！没有什么比行驶安全更重要！</span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><strong style=\"float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">&nbsp;经典内飞版尼罗河游轮旅行 七大神庙+五大景区</span></strong></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【特色主题】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">尼罗河游轮穿越千年文明+浪漫红海度假+古文明探索!<br><span style=\"color:rgb(255, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【五大景区】</span><span style=\"color:rgb(0, 0, 0);position:static;height:auto\">开罗+阿斯旺+卢克索+红海+亚历山大真正全景环游！</span></span><br></span></span><span style=\"color:rgb(255, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【七大神庙】</span><span style=\"color:rgb(0, 0, 0);position:static;height:auto\">六大经典神庙入内(两游轮专享)+可选阿布辛贝神庙！<br><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【重要景点】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">金字塔+狮身人面像+埃及博物馆一个都不能少！</span></span></span></span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(255, 0, 0);position:static;height:auto\"><span style=\"color:rgb(0, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\"><span style=\"color:rgb(0, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0)\">☆【游轮住宿】</span><span style=\"position:static;height:auto\">尼罗河游轮3晚连住,常年合作品质游轮(河景房标准间)！</span><br></span></span></span></span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【红海度假】</span><span style=\"color:rgb(0, 0, 0);position:static;height:auto\">红海海滨指定卓越度假村3晚连住,真正度假之旅！</span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(255, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【升级内飞】</span><span style=\"color:rgb(0, 0, 0);position:static;height:auto\">升级一段内陆飞机,不乘不能洗澡的夜火车！</span></span><br></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\"><strong style=\"color:rgb(34, 34, 34);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;font-size:14px;white-space:normal;position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">&nbsp;省心预订放心出行&nbsp;包含超千元签证小费等必含费用</span></strong></span></p><p><span style=\"font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;font-size:14px;background-color:rgb(255, 255, 255);color:rgb(192, 0, 0);position:static;height:auto\">☆【便捷签证】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">跟团办理落地签,无需护照原件无需提交材料!</span></span><br><span style=\"font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;font-size:14px;background-color:rgb(255, 255, 255);color:rgb(192, 0, 0);position:static;height:auto\">☆【包含小费】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">含价值900元司导服务小费+尼罗河游轮服务费!<br><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【省心含餐】<span style=\"color:rgb(0, 0, 0);position:static;height:auto\">含埃及境内全程正餐,无自理餐安排,省心放心！</span></span></span></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(255, 0, 0);position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【安全保障】</span><span style=\"color:rgb(0, 0, 0);position:static;height:auto\">多年</span></span>合作当地知名地接社+优质持证导游队伍！</span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><span style=\"color:rgb(192, 0, 0);position:static;height:auto\">☆【服务设备】</span>车载WIFI满足上网需求！</span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"><br></span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\">特别说明：为了丰富行程体验,即日起将赠送尼罗河风帆船项目更改为赠送卢克索乘马车晨游底比斯古都，变更不再单独通知。</span></p><p style=\"margin-top:0px;margin-bottom:0px;padding:0px;color:rgb(34, 34, 34);font-size:14px;white-space:normal;background-color:rgb(255, 255, 255);font-family:Arial, &quot;Lucida Grande&quot;, Verdana, &quot;Microsoft YaHei&quot;, hei;float:none;position:static;height:auto\"><span style=\"position:static;height:auto\"></span></p><p><img imageid=\"21313898\" src=\"//dimg04.c-ctrip.com/images/30050o000000f6rizD972.jpg\" data-src=\"//dimg04.c-ctrip.com/images/30050o000000f6rizD972.jpg\" title=\"A-NEW.jpg\" imageauthorize=\"21313898图片有效-有效期\" style=\"opacity: 1;\"> &nbsp; <br></p></div>",
    "fees": "<div class=\"bd\"><dl class=\"mod_info_box\"><dt>费用包含</dt><dd><div class=\"tour_description_table_box\"><table class=\"tour_description_table\"><tbody><tr><th>大交通</th><td><p>往返含税经济舱机票</p></td></tr><tr><th>住宿</th><td><p>行程所列酒店住宿费用</p><p>酒店标准2人间</p></td></tr><tr><th>餐食</th><td><p>行程内所列餐食，具体情况请见行程推荐/安排、飞机餐是否收费请参照航空公司规定</p></td></tr><tr><th>门票及地面项目</th><td><p>行程中所列景点首道大门票旅游用车</p></td></tr><tr><th>随团服务人员</th><td><p>中文领队和当地中文导游服务</p></td></tr><tr><th>儿童价标准</th><td><p>年龄2-12周岁（不含），不占床，服务标准同成人</p></td></tr></tbody></table></div></dd></dl><dl class=\"mod_info_box\"><dt>自理费用</dt><dd><div class=\"tour_description_table_box\"><table class=\"tour_description_table\"><tbody><tr><th>儿童附加费</th><td><p>团队中儿童的价格均为不占床含早餐的价格，如需占床，请在预订后续页面中选择儿童占床补差可选项；1位成人携带1位儿童出行，儿童必须占床，请选择儿童占床补差可选项。</p></td></tr><tr><th>补充</th><td><p>出入境个人物品海关征税; 超重行李的托运费、保管费;  酒店内洗衣、理发、电话、传真、收费电视、饮品、烟酒等个人消费; 自由活动期间的用车服务; 提供导游服务的产品在自由活动期间无陪同服务; 当地参加的自费以及“费用包含”中不包含的其它项目</p><p>单房差</p></td></tr></tbody></table></div></dd></dl><dl class=\"mod_info_box\"><dt>推荐活动参考 （需自费）</dt><dd><div class=\"tour_self_table_box\"><table class=\"tour_self_table\"><tbody><tr><th style=\"width: 170px;\">活动</th><th style=\"width: 110px;\">参考价格</th><th>说明</th></tr><tr><td>菲莱神庙声光秀</td><td>70美金/人（2-5人）</td><td>70美金/人（2-5人）65美金/人（6-9人）60美金/人（10人及以上）费用包含：车费、导游费用、景点门票</td></tr><tr><td>金字塔声光秀</td><td>75美金/人（2-5人）</td><td>在现代声与光的结合下，感受4千多年前的历史沧桑。含接送服务，中文导游陪同以及门票。<br>75美金/人（2-5人）<br>65美金/人（6人以上）<br></td></tr><tr><td>夜游尼罗河</td><td>85美金/人（4-9人）</td><td>晚上乘坐尼罗河游船，欣赏两岸风光，并在船上享用晚餐（不含酒水饮料），欣赏当地特色表演（斋月期间表演暂停）。包含码头接送服务，以及中文导游陪同服务。<br>85美金/人（4-9人）<br> 75美金/人（10人及以上）<br></td></tr><tr><td>阿布辛贝神庙</td><td>145美金/人</td><td>早上约4点左右出发，在沙漠护卫队下前往和返回。阿布辛贝神庙是阿斯旺的旅游重点。是古埃及伟大的法老拉美西斯二世（ Ramses Ⅱ）所建，也是新帝国的法老王时代受保护的遗迹。包含车费，中文导游陪同和讲解服务以及景点门票<br>145美金/人（6-9人）<br>140美金/人（10-14人）<br>125美金/人（15人及以上）<br></td></tr><tr><td>阿斯旺努比亚村游览</td><td>50美金/人（4-7人）</td><td>搭乘小船前往阿斯旺特有的“少数民族”村落--努比亚村。在这里可以体验到古老的努比亚文明，参观努比亚人特有的彩色房子，学习当地语言，并参观当人家。包含码头接送服务，中文导游陪同以及努比亚村特色饮料和骑骆驼。<br>50美金/人（4-7人）<br>45美金/人（8人及以上）<br></td></tr><tr><td>四驱吉普冲沙</td><td>90美金/人（4-7人）</td><td>下午2点半左右，搭乘四驱车从酒店出发，前往埃及特有的东部隔壁沙漠冲沙。在空旷的隔壁中放飞自我。爬上沙丘顶端欣赏日落。之后前往古老的贝都因人村落，一探贝都因人的生活。并体验骑骆驼的乐趣。返程途中幸运的话还可以看到满天繁星。<br>注意：此项目为刺激性项目。四驱车行驶过程中较为颠簸，存在一定风险性，老弱妇孺及病患请慎重参加！上下骆驼请注意安全！若用车座椅未配备安全带，请您拒绝上车并要求退还相应费用！<br>90美金/人（4-7人）<br>80美金/人（8人以上）<br>费用包含：4*4吉普车费、导游费用、景点门票、BBQ烤肉晚餐</td></tr><tr><td>吉夫顿岛游览</td><td>80美金/人（10人以上）</td><td>早上8点半左右从酒店出发，前往码头，登上游艇，进入美丽的红海。包船出海不与其他游客拼船，尽享红海风景。喂海鸥，钓鱼，浮潜各项游乐随心选择。游艇上提供浮潜设备，钓鱼基本设备。中午在船上享用简单午餐。包括接送，中文导游陪同服务。<br>注意：<br>乘坐游艇出海上下船时请注意安全，依次排队切勿拥挤、小心地滑。船长和救生员未作出安排前，切勿做出危险性动作。由于游艇速度较快，海上较为颠簸，老弱妇孺及病患请慎重参加！）<br>80美金/人（10人以上）<br></td></tr><tr><td>辛巴达号潜艇</td><td>115美金/人（2人起）</td><td>前往码头搭乘快艇前往潜水艇平台，搭乘潜水艇潜入7米深红海，欣赏神秘美丽的红海海底世界。并有潜水员为您献上海底喂鱼的表演。含接送，中文导游陪同<br>注意：<br>此项目为刺激性项目，由于海下具有一定压强，老弱妇孺及病患请慎重参加！<br>115美金/人（2人起）</td></tr><tr><td>红海玻璃船游览</td><td>70美金/人（4人起）</td><td>搭乘特殊定制的游船，在游船底部设有大型观光窗，便于欣赏奇妙的海底世界。包含接送，中文导游陪同<br>注意：<br>上下船时请注意安全，依次排队切勿拥挤、小心地滑。<br>70美金/人（4人起）</td></tr><tr><td>卢克索热气球</td><td>165美金/人（2-3人）</td><td>早上5点左右从酒店出发前往码头，搭乘小船前往尼罗河西岸。小船上准备有热咖啡，茶，以及小点心。搭乘热气球迎接日出，并俯瞰卢克索。途径哈布城，女王神庙，帝王谷等景点，从高空体验不一样的卢克索。落地后会举办一个小的庆祝仪式，并为客人颁发证书。之后专车送返酒店。<br>特别提示：<br>1.热气球项目为高风险项目，请根据自身情况谨慎选择参加。<br>2.行程安排仅供参考，视当天具体天气情况而定。若因天气状况而无法乘坐热气球，则原价退还！<br>3.小童不满7岁无法参加此项目<br>4.热气球期间，领队与导游全程不陪同。上下热气球时请按次序耐心等待，切勿着急上下热气球而作出危险动作，以免发生意外。且飞且珍惜！165美金/人（2-3人）<br><br>150美金/人（4人及以上）</td></tr><tr><td colspan=\"3\">以上所列项目均是建议性项目，客人本着“自愿自费”的原则选择参加，部分项目参加人数不足或资源不足时，可能无法成行。</td></tr></tbody></table></div></dd></dl></div>",
    "notes": "<div class=\"bd\"><dl class=\"mod_info_box\"><dt>费用包含</dt><dd><div class=\"tour_description_table_box\"><table class=\"tour_description_table\"><tbody><tr><th>大交通</th><td><p>往返含税经济舱机票</p></td></tr><tr><th>住宿</th><td><p>行程所列酒店住宿费用</p><p>酒店标准2人间</p></td></tr><tr><th>餐食</th><td><p>行程内所列餐食，具体情况请见行程推荐/安排、飞机餐是否收费请参照航空公司规定</p></td></tr><tr><th>门票及地面项目</th><td><p>行程中所列景点首道大门票旅游用车</p></td></tr><tr><th>随团服务人员</th><td><p>中文领队和当地中文导游服务</p></td></tr><tr><th>儿童价标准</th><td><p>年龄2-12周岁（不含），不占床，服务标准同成人</p></td></tr></tbody></table></div></dd></dl><dl class=\"mod_info_box\"><dt>自理费用</dt><dd><div class=\"tour_description_table_box\"><table class=\"tour_description_table\"><tbody><tr><th>儿童附加费</th><td><p>团队中儿童的价格均为不占床含早餐的价格，如需占床，请在预订后续页面中选择儿童占床补差可选项；1位成人携带1位儿童出行，儿童必须占床，请选择儿童占床补差可选项。</p></td></tr><tr><th>补充</th><td><p>出入境个人物品海关征税; 超重行李的托运费、保管费;  酒店内洗衣、理发、电话、传真、收费电视、饮品、烟酒等个人消费; 自由活动期间的用车服务; 提供导游服务的产品在自由活动期间无陪同服务; 当地参加的自费以及“费用包含”中不包含的其它项目</p><p>单房差</p></td></tr></tbody></table></div></dd></dl><dl class=\"mod_info_box\"><dt>推荐活动参考 （需自费）</dt><dd><div class=\"tour_self_table_box\"><table class=\"tour_self_table\"><tbody><tr><th style=\"width: 170px;\">活动</th><th style=\"width: 110px;\">参考价格</th><th>说明</th></tr><tr><td>菲莱神庙声光秀</td><td>70美金/人（2-5人）</td><td>70美金/人（2-5人）65美金/人（6-9人）60美金/人（10人及以上）费用包含：车费、导游费用、景点门票</td></tr><tr><td>金字塔声光秀</td><td>75美金/人（2-5人）</td><td>在现代声与光的结合下，感受4千多年前的历史沧桑。含接送服务，中文导游陪同以及门票。<br>75美金/人（2-5人）<br>65美金/人（6人以上）<br></td></tr><tr><td>夜游尼罗河</td><td>85美金/人（4-9人）</td><td>晚上乘坐尼罗河游船，欣赏两岸风光，并在船上享用晚餐（不含酒水饮料），欣赏当地特色表演（斋月期间表演暂停）。包含码头接送服务，以及中文导游陪同服务。<br>85美金/人（4-9人）<br> 75美金/人（10人及以上）<br></td></tr><tr><td>阿布辛贝神庙</td><td>145美金/人</td><td>早上约4点左右出发，在沙漠护卫队下前往和返回。阿布辛贝神庙是阿斯旺的旅游重点。是古埃及伟大的法老拉美西斯二世（ Ramses Ⅱ）所建，也是新帝国的法老王时代受保护的遗迹。包含车费，中文导游陪同和讲解服务以及景点门票<br>145美金/人（6-9人）<br>140美金/人（10-14人）<br>125美金/人（15人及以上）<br></td></tr><tr><td>阿斯旺努比亚村游览</td><td>50美金/人（4-7人）</td><td>搭乘小船前往阿斯旺特有的“少数民族”村落--努比亚村。在这里可以体验到古老的努比亚文明，参观努比亚人特有的彩色房子，学习当地语言，并参观当人家。包含码头接送服务，中文导游陪同以及努比亚村特色饮料和骑骆驼。<br>50美金/人（4-7人）<br>45美金/人（8人及以上）<br></td></tr><tr><td>四驱吉普冲沙</td><td>90美金/人（4-7人）</td><td>下午2点半左右，搭乘四驱车从酒店出发，前往埃及特有的东部隔壁沙漠冲沙。在空旷的隔壁中放飞自我。爬上沙丘顶端欣赏日落。之后前往古老的贝都因人村落，一探贝都因人的生活。并体验骑骆驼的乐趣。返程途中幸运的话还可以看到满天繁星。<br>注意：此项目为刺激性项目。四驱车行驶过程中较为颠簸，存在一定风险性，老弱妇孺及病患请慎重参加！上下骆驼请注意安全！若用车座椅未配备安全带，请您拒绝上车并要求退还相应费用！<br>90美金/人（4-7人）<br>80美金/人（8人以上）<br>费用包含：4*4吉普车费、导游费用、景点门票、BBQ烤肉晚餐</td></tr><tr><td>吉夫顿岛游览</td><td>80美金/人（10人以上）</td><td>早上8点半左右从酒店出发，前往码头，登上游艇，进入美丽的红海。包船出海不与其他游客拼船，尽享红海风景。喂海鸥，钓鱼，浮潜各项游乐随心选择。游艇上提供浮潜设备，钓鱼基本设备。中午在船上享用简单午餐。包括接送，中文导游陪同服务。<br>注意：<br>乘坐游艇出海上下船时请注意安全，依次排队切勿拥挤、小心地滑。船长和救生员未作出安排前，切勿做出危险性动作。由于游艇速度较快，海上较为颠簸，老弱妇孺及病患请慎重参加！）<br>80美金/人（10人以上）<br></td></tr><tr><td>辛巴达号潜艇</td><td>115美金/人（2人起）</td><td>前往码头搭乘快艇前往潜水艇平台，搭乘潜水艇潜入7米深红海，欣赏神秘美丽的红海海底世界。并有潜水员为您献上海底喂鱼的表演。含接送，中文导游陪同<br>注意：<br>此项目为刺激性项目，由于海下具有一定压强，老弱妇孺及病患请慎重参加！<br>115美金/人（2人起）</td></tr><tr><td>红海玻璃船游览</td><td>70美金/人（4人起）</td><td>搭乘特殊定制的游船，在游船底部设有大型观光窗，便于欣赏奇妙的海底世界。包含接送，中文导游陪同<br>注意：<br>上下船时请注意安全，依次排队切勿拥挤、小心地滑。<br>70美金/人（4人起）</td></tr><tr><td>卢克索热气球</td><td>165美金/人（2-3人）</td><td>早上5点左右从酒店出发前往码头，搭乘小船前往尼罗河西岸。小船上准备有热咖啡，茶，以及小点心。搭乘热气球迎接日出，并俯瞰卢克索。途径哈布城，女王神庙，帝王谷等景点，从高空体验不一样的卢克索。落地后会举办一个小的庆祝仪式，并为客人颁发证书。之后专车送返酒店。<br>特别提示：<br>1.热气球项目为高风险项目，请根据自身情况谨慎选择参加。<br>2.行程安排仅供参考，视当天具体天气情况而定。若因天气状况而无法乘坐热气球，则原价退还！<br>3.小童不满7岁无法参加此项目<br>4.热气球期间，领队与导游全程不陪同。上下热气球时请按次序耐心等待，切勿着急上下热气球而作出危险动作，以免发生意外。且飞且珍惜！165美金/人（2-3人）<br><br>150美金/人（4人及以上）</td></tr><tr><td colspan=\"3\">以上所列项目均是建议性项目，客人本着“自愿自费”的原则选择参加，部分项目参加人数不足或资源不足时，可能无法成行。</td></tr></tbody></table></div></dd></dl></div>",
    "rating": 3.2,
    "travelDays": "Three",
    "tripType": "BackPackTour",
    "departureCity": "Shenzhen",
    "touristRoutePictures": [
        {
            "id": 28,
            "url": "../../assets/images/louvre-102840_640.jpg",
            "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"
        },
        {
            "id": 29,
            "url": "../../assets/images/louvre-102840_640.jpg",
            "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"
        },
        {
            "id": 30,
            "url": "../../assets/images/louvre-102840_640.jpg",
            "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"
        },
        {
            "id": 31,
            "url": "../../assets/images/louvre-102840_640.jpg",
            "touristRouteId": "39996f34-013c-4fc6-b1b3-0c1036c47110"
        }
    ]
}
```





## 部分更新旅游路线信息

本接口用于部分更新旅游路线信息，包括修改标题、修改图片等操作。



### 请求路径

```
textCopy code
http://106.14.174.76:8080/api/touristRoutes/39996f34-013c-4fc6-b1b3-0c1036c47110

```

### 请求方法

```
textCopy code
PATCH

```

### 请求参数

本接口接受 JSON 格式的请求体。

```
jsonCopy code
[
    {
        "op": "replace",
        "path": "/title",
        "value": "ABCDEFG"
    },
    {
        "op": "replace",
        "path": "/touristRoutePictures/0/url",
        "value": "../../assets/images/fake.jpg"
    }
]

```

请求参数说明如下：

| 参数名称  | 类型     | 是否必须 | 描述                         |
| ----- | ------ | ---- | -------------------------- |
| op    | string | 是    | 更新操作类型，本接口固定为 "replace"    |
| path  | string | 是    | 更新的属性路径，例如 "/title" 表示更新标题 |
| value | any    | 是    | 更新的属性值                     |

本接口支持部分更新，即只更新指定的属性。例如上述请求体表示更新标题为 "ABCDEFG"，并将第一张图片的 URL 更新为 "../../assets/images/fake.jpg"。

### 请求头

本接口需要在请求头中添加访问令牌，用于身份验证和授权。

```
textCopy code
Authorization: Bearer [access_token]

```

access_token 为通过登录认证后获取的访问令牌。

### 响应信息

### 响应状态码

| 状态码  | 说明    |
| ---- | ----- |
| 204  | 更新成功  |
| 401  | 未授权   |
| 404  | 未找到路线 |

### 响应头

本接口返回空响应体。

### 响应示例

```
textCopy code
HTTP/1.1 204 No Content

```

### 错误信息

### 错误响应

| 错误码  | 错误信息                    | 说明      |
| ---- | ----------------------- | ------- |
| 401  | Unauthorized            | 未授权     |
| 404  | Tourist route not found | 未找到旅游路线 |

### 返回结果说明

本接口不返回响应体，只返回状态码。





## 根据ID删除旅游路线

接口路径：[http://106.14.174.76:8080/api/touristRoutes/{id}](http://106.14.174.76:8080/api/touristRoutes/%7Bid%7D)

请求方式：DELETE

请求参数：

| 参数名  | 参数类型   | 参数说明   |
| ---- | ------ | ------ |
| id   | string | 旅游路线ID |

请求示例：<http://106.14.174.76:8080/api/touristRoutes/fb6d4f10-79ed-4aff-a915-4ce29dc9c7e1>

请求头：

| 参数名           | 参数类型   | 参数说明         |
| ------------- | ------ | ------------ |
| Authorization | string | Bearer Token |

请求示例：Authorization: Bearer [access_token]

响应体：无响应状态：204

响应示例：HTTP/1.1 204 No Content

错误响应：HTTP/1.1 401 Unauthorized{"code": "Unauthorized","message": "Authentication failed"}HTTP/1.1 404 Not Found{"code": "NotFound","message": "The tourist route with the provided id was not found"}
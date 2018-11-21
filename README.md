# jm-log

**日志系统**

[TOC]

## use:

```javascript
var s = require('jm-log')();
```



## run:

```javascript
npm start
```



## 配置参数

基本配置 请参考 [jm-server] (https://github.com/jm-root/ms/tree/master/packages/jm-server)

db [] mongodb服务器Uri

table_name_prefix [''] 表名称前缀



## 获取日志列表

接口地址：/log/logs

请求方式：GET

请求参数：

| 参数名称  | 参数类型 | 必填 | 默认值 | 可选值 | 参数说明                                     |
| --------- | -------- | ---- | ------ | ------ | -------------------------------------------- |
| page      | integer  | 否   | 1      | 正整数 | 第几页                                       |
| rows      | integer  | 否   | 20     | 正整数 | 每页几行                                     |
| level     | integer  | 否   | 1      | 0~4    | 日志等级；0~4：debug info warn error fatal |
| startTime | integer  | 否   |        |        | 起始时间戳                                   |
| endTime   | integer  | 否   |        |        | 截止时间戳                                   |
| search    | string   | 否   |        |        | 对 title 进行模糊查询                        |

请求示例：

```json
{
  "page": 1,
  "rows": 20,
  "level": 1,
  "startTime": 1542762880,
  "endTime": 1542762886,
  "search": "/image_codes/"
}
```



返回json数据，参数：

| 参数名称   | 参数类型 | 可能值 | 参数说明                                   |
| ---------- | -------- | ------ | ------------------------------------------ |
| page       | integer  |        | 当前页码                                   |
| total      | integer  |        | 总行数                                     |
| pages      | integer  |        | 总页数                                     |
| rows       | array    |        | 返回数据                                   |
| rows/id    | string   |        | userId                                     |
| rows/level | integer  | 0~4    | 日志等级；0~4：debug info warn error fatal |
| rows/ip    | string   |        | IP地址                                     |
| rows/title | string   |        | 日志内容                                   |

返回示例：

```json
{
  "rows": [
    {
      "id": "string",
      "level": 1,
      "ip": "59.42.239.129",
      "title": "INFO 2018-11-21 09:14:40,576 basehttp 124 'GET /image_codes/b4c01dd6-9007-4b9b-983e-4057d452136b/ HTTP/1.1' 200 3568"
    },
    {
      "id": "string",
      "level": 1,
      "ip": "59.42.239.129",
      "title": "INFO 2018-11-21 09:14:45,576 basehttp 124 'GET /image_codes/abcac98e-4fb4-4dce-bbe8-07340211a22e/ HTTP/1.1' 200 3134"
    }
  ],
  "page": 1,
  "total": 2,
  "pages": 1
}
```



## 新增日志

接口地址：/log/logs

请求方式：POST

请求参数：

| 参数名称 | 参数类型 | 必填 | 默认值 | 可选值 | 参数说明                                   |
| -------- | -------- | ---- | ------ | ------ | ------------------------------------------ |
| id       | string   | 否   |        |        | userId                                     |
| level    | integer  | 否   | 1      | 0~4    | 日志等级；0~4：debug info warn error fatal |
| ip       | string   | 否   |        |        | IP地址                                     |
| title    | string   | 是   |        |        | 日志内容                                   |

请求示例：

```json
{
  "id": "fs2fee",
  "level": 1,
  "ip": "59.42.239.129",
  "title": "INFO 2018-11-21 10:32:39,159 basehttp 124 'GET /abc/ HTTP/1.1 201 39"
}
```



返回json数据，参数：

| 参数名称 | 参数类型 | 可能值 | 参数说明         |
| -------- | -------- | ------ | ---------------- |
| ret      | integer  | 0\|1   | 1：成功；0：失败 |
| id       | string   |        | userId           |

返回示例：

```json
{
  "ret": 1,
  "id": "fs2fee"
}
```



## 获取指定日志

接口地址：/log/logs/{id}

请求方式：GET

请求参数：

| 参数名称 | 参数类型 | 必填 | 默认值 | 可选值 | 参数说明 |
| -------- | -------- | ---- | ------ | ------ | -------- |
| id       | string   | 是   |        |        | userId   |



返回json数据，参数：

| 参数名称 | 参数类型 | 可能值 | 参数说明                                   |
| -------- | -------- | ------ | ------------------------------------------ |
| id       | string   |        | userId                                     |
| level    | integer  | 0~4    | 日志等级；0~4：debug info warn error fatal |
| ip       | string   |        | IP地址                                     |
| title    | string   |        | 日志内容                                   |

返回示例：

```json
{
  "id": "fs2fee",
  "level": 1,
  "ip": "59.42.239.129",
  "title": "INFO 2018-11-21 10:32:39,159 basehttp 124 'GET /abc/ HTTP/1.1 201 39"
}
```



## 删除指定日志

接口地址：/log/logs/{id}

请求方式：DELETE

请求参数：

| 参数名称 | 参数类型 | 必填 | 默认值 | 可选值 | 参数说明 |
| -------- | -------- | ---- | ------ | ------ | -------- |
| id       | string   | 是   |        |        | userId   |



返回json数据，参数：

| 参数名称 | 参数类型 | 可能值 | 参数说明         |
| -------- | -------- | ------ | ---------------- |
| ret      | integer  | 0\|1   | 1：成功；0：失败 |

返回示例：

```json
{
  "ret": 1
}
```






















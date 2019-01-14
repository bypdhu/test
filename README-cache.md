# 缓存刷新

| Date      | Version | Owner | Comments    |
| --------- | ------- | ----- | ----------- |
| 2019.1.14 | v1.0.0 | bian  | Created it. |


## 一、 简介

### 1. 功能 
CND刷新URL和目录，目前支持阿里云和网宿。

### 2. 准备
#### 2.1 运维人员创建应用key
后台-CDN管理-应用key-新建
#### 2.2 获取程序地址
?


## 二、 使用

### 1. CDN刷新URL和目录

#### 1.1 参数

| 参数名称      | 类型 | 说明 | 
| --------- | ------- | -------------------------- |
| urls | 列表 | 每个URL必须以'http://' 或 'https://' 开头。 _*注意：urls和dirs不能同时为空。*_ |
| dirs | 列表 | 每个目录必须以'http(s)://域名/'开始，以'/'结尾。 _*注意：urls和dirs不能同时为空。*_ |
| uuid | 字符串 | 必填，填入应用key。请联系运维获取。 |

#### 1.2 说明
- 生效时间： 约5-10分钟
- 阿里云限制说明： 同一个ID每天最多提交预热刷新类请求数量：URL 2000条， 目录 100个。
- 网宿限制说明： 刷新url每日不超过5000条，刷新目录每日不超过500条，每次接口调用url和目录总数不超过500条。 调用频率：10/5min。

#### 1.3 http示例

**请求语法**
```
POST [地址]/api/v2/cdn/refreshcaches HTTP/1.1 
Content-Type: application/json
```
```json
{
  "dirs": [
    "http://test1.com/1/",
    "http://test2.com/2/"
  ],
  "urls": [
    "http://test3.com/1.png",
    "http://test4.com/2.png"
  ],
  "uuid": "string" //必填
}
```

**返回体（成功)**
```
Content-Type: application/json
```
```json
{
  "code": 1,
  "message": "success",
  "data": null
}
```
**返回体（失败)**

```
Content-Type: application/json
```
```json
{
  "code": 0,
  "message": "failure",
  "data": "urls 和 dirs 不能同时为空"
}
```

#### 1.4 curl示例
```bash
curl -X POST "http://[地址]/api/v2/cdn/refreshcaches" -H "accept: */*" -H "Content-Type: application/json" -d "{ \"urls\": [\"http://test1.com/1.png\",\"http://test2.com/2.png\" ], \"uuid\": \"your appKey\"}"
```
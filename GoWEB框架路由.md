# GoWEB框架和路由

## Goweb

### web应用流程

![](C:\Users\86181\AppData\Roaming\marktext\images\2023-02-06-14-48-31-image.png)**goweb使用默认的多路复用器去转发请求到处理器，如果要使用模板，处理器解析并渲染返回响应，和数据交互通过模型完成**

## RESTful API

**网站的设计遵循RESTful原则**

## Echo

**简单易用的go web框架之一**

### 路由&控制器

**路由是一个过程，指的是一个http请求，如何找到对应的控制器函数**

**控制器函数主要负责执行http请求-响应任务**

```go
/*实例*/
//路由定义POST请求，url路径为:/users,绑定saveUser控制器函数
e.POST("/users",saveUser)
//控制器函数
func saveUser(c echo.Context) error {
    username :=c.FormValue("username")
    //调用model保存数据
    html:=调用模板引擎渲染html页面
    //以Html页面的形式响应请求
    return c.HTML(http.StatusOK,html)
}
```

#### 路由规则

**路由规则通常由三部分组成：**

* http请求方法（GET/POST/PUT/DELETE）

* url路径

* 控制器函数

##### url路径

* 静态url路径

* 带路径参数的url路径

* 带星号(*)模糊匹配参数的url路径
  
  ```go
  //ep1 静态url路径，即不带任何参数的url
  /users/center
  /users/101
  //ep2 带路径参数的url路径，url路径上面带有参数，参数由冒号跟一个字符串定义
  /users/:id
  //带星号的模糊匹配url路径，可以匹配任何路径
  ```

**当http请求匹配到多个定义的url路径，按照静态、带参、星号的顺序匹配**

#### 控制器函数

```go
//定义
func HandlerFunc(c echo.Context) error
//控制器函数接受一个上下文参数，并返回一个错误
//可以通过上下文参数，获取http请求参数，响应http请求
```

### 处理请求参数

## Gin

**简单易用的go web框架之一**

```go
package main

import (
    "gtihub.com/gin-gonic/gin"
)

func main(){
    //创建一个默认的路由引擎
    r:=gin.Default()
    //GET:请求方式；/hello：请求路径
    //当客户端以GET方法请求/hello路径的时候，会执行后面的匿名函数
    r.GET("/hello",func(c *gin.Context)

}
```

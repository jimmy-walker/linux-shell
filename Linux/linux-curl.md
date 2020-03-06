# Brief

curl 是常用的命令行工具，用来请求 Web 服务器。**它的名字就是客户端（client）的 URL 工具的意思**。 

# Command

##不带有任何参数

不带有任何参数时，curl 就是发出 GET 请求。

> ```linux
> curl https://www.example.com
> ```

## **-d**(data)

`-d`参数用于发送 POST 请求的数据体。

> ```
> $ curl -d 'login=emma＆password=123'-X POST https://google.com/login
> # 或者
> $ curl -d 'login=emma' -d 'password=123' -X POST  https://google.com/login
> ```

使用`-d`参数以后，HTTP 请求会自动加上标头`Content-Type : application/x-www-form-urlencoded`。并且**会自动将请求转为 POST 方法，因此可以省略`-X POST`**。

## **-H**(header)

`-H`参数添加 HTTP 请求的标头。

> ```
> $ curl -H 'Accept-Language: en-US' https://google.com
> ```

上面命令添加 HTTP 标头`Accept-Language: en-US`。

> ```
> $ curl -H 'Accept-Language: en-US' -H 'Secret-Message: xyzzy' https://google.com
> ```

上面命令添加两个 HTTP 标头。

> ```
> $ curl -d '{"login": "emma", "pass": "123"}' -H 'Content-Type: application/json' https://google.com/login
> ```

上面命令添加 HTTP 请求的标头是`Content-Type: application/json`，然后用`-d`参数发送 JSON 数据。

## **-I**(info)

`-I`参数向服务器发出 HEAD 请求，然会将服务器返回的 HTTP 标头打印出来。

> ```
> $ curl -I https://www.example.com
> ```

上面命令输出服务器对 HEAD 请求的回应。



## -X**(request)

`-X`参数指定 HTTP 请求的方法。

> ```
> $ curl -X POST https://www.example.com
> ```

上面命令对`https://www.example.com`发出 POST 请求。

# Reference

- [curl 的用法指南](https://www.ruanyifeng.com/blog/2019/09/curl-reference.html )
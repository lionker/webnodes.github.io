//设置路由
/*
  路由：
    1. 作用：
      - 定义请求地址
      - 处理请求、返回响应
    2. 组成：
      - 请求方式： GET(查) POST(增) PUT(改) DELETE(删)
      - 路由路径： 定义请求地址
        基本 /   /login /shop/a  一个url网址对应一个路由
        特殊 /xxx/:xxx   多个url网址对应一个路由(:后面的值可变)
      - 若干个回调函数（句柄函数）
        request 请求信息， 浏览器发送服务器的
        response 响应信息, 服务器发给浏览器
    3. 是什么
      - key-value的映射关系 key是路由路径，value是回调函数
    4. 执行顺序
      从上到下，依次检查是否匹配上了路由，如果有就执行相应的回调函数，如果没有匹配上就看下一个
      如果都没有匹配上。返回404
      
 */
 
 1、定义路由

URL地址里面的index模块怎么才能省略呢，默认的URL地址显得有点长，下面就来说说如何通过路由简化URL访问。
我们在路由定义文件（application/route.php）里面添加一些路由规则，如下

默认URL访问为

http://www.peace52.com/index/index/hello/name/zhangsan.html

改造后

http://www.peace52.com/hello/zhangsan.html

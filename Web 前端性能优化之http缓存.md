### http缓存
  #### 浏览器请求数据有时会重复请求相同的数据，会产生大量没有必要的网络请求，拖慢浏览器的资源加载速度，影响用户体验
  通过设置http header的属性，来设置浏览器缓存从而来降低网络请求，避免浏览器发起不必要的请求，以至于浏览器重新下载资源
* http的缓存策略有三种，一般为:仅设置max-age，设置max-age和Last-modified(If-modified-since),设置max-age和Etag。
1. 仅仅设置max-age(这种比较简单)
    * 只需要设置http header的Cache-control: max-age=10*60 (单位为秒) 
    * 浏览器的执行过程为：
      * 第一步：
        1. 浏览器第一次请求资源`http://www.xxx.com/index.js`
        2. 浏览器查询临时文件目录发现无cache内容，于是发出请求到web server
        3. Web server接到请求，响应资源，并设定`http://www.xxx.com/index.js`
        4. 浏览器接到响应，将内容展示的同时，在临时文件目录以`“http://www.xxx.com/index.js”`为key缓存这个响应的内容
      * 第二步：
        1. 离第一步请求间隔时间不到10分钟
        2. 浏览器再次请求资源`http://www.xxx.com/index.js`
        3. 浏览器查询临时文件目录发现有cache内容，于是检查max-age，还未过期，直接读取，响应给用户。（HTTP状态“(Cache)”）
      * 第三步：
        1. 离第一步请求间隔时间已超过10分钟
        2. 浏览器再次请求资源`http://www.xxx.com/index.js`
        3. 浏览器查询临时文件目录发现有cache内容，于是检查max-age，已经过期，发起请求给web server。（HTTP状态“200”）
2. 设置max-age和Last-modified(If-modified-since)
3. 设置max-age和Etag
    

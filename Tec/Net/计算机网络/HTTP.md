```
content-length:编码后全部报文的长度
其实后面几条几乎可以忽视，简单总结后如下：
1、Content-Length如果存在并且有效的话，则必须和消息内容的传输长度完全一致。（经过测试，如果过短则会截断，过长则会导致超时。）
2、如果存在Transfer-Encoding（重点是chunked），则在header中不能有Content-Length，有也会被忽视。
3、如果采用短连接，则直接可以通过服务器关闭连接来确定消息的传输长度。（这个很容易懂）
结合HTTP协议其他的特点，比如说Http1.1之前的不支持keep alive。那么可以得出以下结论：
1、在Http 1.0及之前版本中，content-length字段可有可无。
2、在http1.1及之后版本。如果是keep alive，则content-length和chunk必然是二选一。若是非keep alive，则和http1.0一样。content-length可有可无。  
```
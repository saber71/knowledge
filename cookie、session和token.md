# 不同点

### 存储位置不同

cookie由浏览器负责保存和管理，在发送请求时浏览器会自动写入请求头中

session存储在后端，通常是内存或数据库

token存在客户端，通常以加密的方式存在localStorage或sessionStorage

### 数据安全性不同

cookie因为存在客户端所以存在窃取和篡改的风险，需要对数据进行加密

session存在后端，通过一个sessionID在客户端和后端之间进行关联，避免数据暴露

token通常使用加密算法生成，有效期短且不可逆，有较高的安全性

### 跨域支持不同

cookie出于安全考虑，不支持跨域

session通常将sessionID存在cookie中，所以通常是不支持跨域的。但是如果将sessionID写在其他地方（比如拼接在url里），则是可以做到跨域的

token本身是写在请求头中发送给后端的，是可以跨域的。但token通常是存在浏览器的localStorage里，想跨域获取到localStorage中的内容则需要想办法（比如获取到那个页面的window对象，通过postMessage主动发送给另一个页面）

### 应用场景不同

cookie是一种临时数据，是用于实现状态管理的一种机制

session是后端记录用户状态的一种方式，服务器为每一个会话分配一个唯一的id并将其与用户状态相关联

token是一种认证和授权的机制，通常表示用户的身份和权限信息
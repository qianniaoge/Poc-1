- [S2-059][CVE-2019-0230](https://cwiki.apache.org/confluence/display/WW/S2-059)
- [S2-061][CVE-2020-17530](https://cwiki.apache.org/confluence/display/WW/S2-061)

[S2-059]影响版本：
2.0.0 - 2.5.20

[S2-061]影响版本：
2.0.0 - 2.5.25

漏洞描述：
> 如果开发人员使用了 %{…} 语法，那么攻击者可以通过构造恶意的  OGNL  表达式，引发  OGNL  表达式二次解析，最终造成远程代码执行的影响。




参考：
- [CVE-2019-0230： S2-059 远程代码执行漏洞分析](https://mp.weixin.qq.com/s/AIIEE_Ril49WAoyDp64_og)
- [CVE-2019-0230 s2-059 漏洞分析](https://www.cnblogs.com/ph4nt0mer/p/13512599.html)
- [CVE-2019-0233： S2-060 拒绝服务漏洞分析](https://mp.weixin.qq.com/s/OJRxxvD9BnUEyzB0q0Z9yQ)
- https://mp.weixin.qq.com/s/cBZ4P0GIH8jCpGfT2o02Rw


漏洞汇总：
- https://www.sec-note.com/2018/01/09/Struts2-xxx/

批量扫描工具：
- https://github.com/Lucifer1993/struts-scan

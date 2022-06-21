DalFox is an powerful open source XSS scanning tool and parameter analyzer and utility that fast the process of detecting and verify XSS flaws. It comes with a powerful testing engine, many niche features for the cool hacker!

## Key features
Mode: `url` `sxss` `pipe` `file` `server` `payload`

| Class         | Key Feature                   | Description                                                  |
| ------------- | ----------------------------- | ------------------------------------------------------------ |
| Discovery     | Parameter analysis            | - Find reflected param<br />- Find alive/bad special chars, event handler and attack code <br />- Identification of injection points(HTML/JS/Attribute) <br /> `inHTML-none` `inJS-none` `inJS-double` `inJS-single` `inJS-backtick` `inATTR-none` `inATTR-double` `inATTR-single` |
|               | Static analysis               | - Check bad-header like CSP, XFO, etc.. with req/res base    |
|               | BAV analysis                  | - Testing BAV(Basic Another Vulnerability) ,  e.g `sqli` `ssti` `open-redirects`, `crlf`, `esii`    |
|               | Parameter Mining              | - Find new param with Dictonary attack (default is [GF-Patterns](https://github.com/1ndianl33t/Gf-Patterns))<br />- Support custom dictonary file (`--mining-dict-word`)<br />- Find new param with DOM<br />- Use remote wordlist to mining (`--remote-wordlists`) |
|               | Built-in Grepping             | - It Identify the basic info leak of SSTi, Credential, SQL Error, and so on |
|               | WAF Detection and Evasion     | - Detect to WAF(Web Application Firewall). <br />- if found waf and using special flag, evasion using slow request<br />- `--waf-evasion` |
| Scanning      | XSS Scanning                  | - Reflected XSS / Stored XSS / DOM XSS<br />- DOM base verifying<br />- Headless base verifying<br />- Blind XSS testing with param, header(`-b` , `--blind` options)<br />- Only testing selected parameters (`-p`, `--param`)<br />- Only testing parameter analysis (`--only-discovery`) |
|               | Friendly Pipeline             | - Single url mode (`dalfox url`)<br />- From file mode (`dalfox file urls.txt`)<br />- From IO(pipeline) mode (`dalfox pipe`)<br />- From raw http request file mode (`dalfox file raw.txt --rawdata`) |
|               | Optimizaion query of payloads | - Check the injection point through abstraction and generated the fit payload.<br />- Eliminate unnecessary payloads based on badchar |
|               | Encoder                       | - All test payloads(build-in, your custom/blind) are tested in parallel with the encoder.<br />- To Double URL Encoder<br />- To HTML Hex Encoder |
|               | Sequence                      | - Auto-check the special page for stored xss (`--trigger`) <br />- Support (`--sequence`) options for Stored XSS , only `sxss` mode |
| HTTP          | HTTP Options                  | - Overwrite HTTP Method (`-X`, `--method`)<br />- Follow redirects (`--follow-redirects`)<br />- Add header (`-H`, `--header`)<br />- Add cookie (`-C`, `--cookie`)<br />- Add User-Agent (`--user-agent`)<br />- Set timeout (`--timeout`)<br />- Set Delay (`--delay`)<br />- Set Proxy (`--proxy`)<br />- Set ignore return codes (`--ignore-return`)<br />- Load cookie from raw request (`--cookie-from-raw`) |
| Concurrency   | Worker                        | - Set worker's number(`-w`, `--worker`)                      |
|               | N * hosts                     | - Use multicast mode (`--multicast`) , only `file` / `pipe` mode |
| Output        | Output                        | - Only the PoC code and useful information is write as Stdout<br />- Save output (`-o`, `--output`) |
|               | Format                        | - JSON / Plain (`--format`)                                  |
|               | Printing                      | - Silence mode (`--silence`)<br />- You may choose not to print the color (`--no-color`)<br />- You may choose not to print the spinner (`--no-spinner`)<br />- You may choose show only special poc code (`--only-poc`) |
| Extensibility | REST API                      | - API Server and Swagger (`dalfox server`)                   |
|               | Payload Mode                  | - Generate and Enumerate Payloads for XSS Testing (`dalfox payload`) |
|               | Found Action                  | - Lets you specify the actions to take when detected. <br />- Notify, for example (`--found-action`) |
|               | Custom Grepping               | - Can grep with custom regular expressions on response<br />- If duplicate detection, it performs deduplication (`--grep`) |
|               | Custom Payloads               | - Use custom payloads list file (`--custom-payload`) <br />- Custom alert value (`--custom-alert-value`) <br />- Custom alert type (`--custom-alert-type`)|
|               | Remote Payloads               | - Use remote payloads from portswigger, payloadbox, etc.. (`--remote-payloads`)                  |
| Package       | Package manager                | - [pkg.go.dev](https://pkg.go.dev/github.com/hahwul/dalfox/v2)<br/>- [homebrew with tap](https://github.com/hahwul/homebrew-dalfox)<br />- [snapcraft](https://snapcraft.io/dalfox)                                  |
|               | Docker ENV                    | - [docker hub](https://hub.docker.com/repository/docker/hahwul/dalfox)<br />- [gitub package of docker](https://github.com/hahwul/dalfox/packages)     |
|               | Other                         | - [github action](https://github.com/marketplace/actions/xss-scan-with-dalfox) |

And the various options required for the testing :D

## How to Install
### From source
**go1.17**
```
go install github.com/hahwul/dalfox/v2@latest
```

**go1.16**
```
GO111MODULE=on go get github.com/hahwul/dalfox/v2
```

### Using homebrew (macos)
```
brew tap hahwul/dalfox
brew install dalfox
```

### Using snapcraft (ubuntu)
```
sudo snap install dalfox
```

More information? please read [Installation guide](https://dalfox.hahwul.com/docs/installation/)

## Usage
```
▶ dalfox [mode] [target] [flags] 
```

Single target mode
```plain
▶ dalfox url http://testphp.vulnweb.com/listproducts.php\?cat\=123\&artist\=123\&asdf\=ff -b https://hahwul.xss.ht
```

Multiple target mode from file
```plain
▶ dalfox file urls_file --custom-payload ./mypayloads.txt
```

Pipeline mode
```plain
▶ cat urls_file | dalfox pipe -H "AuthToken: bbadsfkasdfadsf87"
```

Other tips, See [wiki](https://github.com/hahwul/dalfox/wiki) for detailed instructions!

## POC format
Sample poc log
```
[POC][G][BUILT-IN/dalfox-error-mysql/GET] http://testphp.vulnweb.com/listproducts.php?artist=123&asdf=ff&cat=123DalFox
[POC][V][GET] http://testphp.vulnweb.com/listproducts.php?artist=123&asdf=ff&cat=123%22%3E%3Csvg%2Fclass%3D%22dalfox%22onLoad%3Dalert%2845%29%3E
```

```
$ go build -o xssapp ; ./xssapp
[] [{V GET https://xss-game.appspot.com/level1/frame?query=%3Ciframe+srcdoc%3D%22%3Cinput+onauxclick%3Dprint%281%29%3E%22+class%3Ddalfox%3E%3C%2Fiframe%3E}] 2.618998247s 2021-07-11 10:59:26.508483153 +0900 KST m=+0.000794230 2021-07-11 10:59:29.127481217 +0900 KST m=+2.619792477}
```

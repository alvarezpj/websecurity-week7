# Project 7 - WordPress Pentesting

Time spent: **15** hours spent in total

> Objective: Find, analyze, recreate, and document **four vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. **Unauthenticated stored cross-site scripting (CVE-2015-3440)** 
  - [X] Summary: 
    - Vulnerability types: XSS  
    - Tested in version: Wordpress 4.2  
    - Fixed in version: [WordPress 4.2.1](https://codex.wordpress.org/Version_4.2.1) 
  - [X] GIF Walkthrough: 
    ![xss-comment1](./xss-e1/xss-1.gif)
    ![xss-comment2](./xss-e1/xss-2.gif)
  - [X] Steps to recreate: 
    - An unauthenticated attacker first injects code as a (long) comment such as [this one](./xss-e1/xss-comment.txt).
    - When an administrator approves and sees the comment, the injected code is executed. 
  - [X] Affected source code:
    - [list of changes](https://core.trac.wordpress.org/changeset?sfp_email=&sfph_mail=&reponame=&new=32311%40branches%2F4.2&old=32300%40branches%2F4.2)
2. **Cross-site scripting in media upload when file too large** 
  - [X] Summary: 
    - Vulnerability types: XSS
    - Tested in version: WordPress 4.7.2
    - Fixed in version: [WordPress 4.7.5](https://codex.wordpress.org/Version_4.7.5)
  - [X] GIF Walkthrough: 
    ![xss-upload](xss-e2/xss.gif)
  - [X] Steps to recreate: 
    - An attacker injects a malicious script into the filename of a large file. The file must exceed WordPress' maximum upload size.
    - The attacker then lures an administrator of the site to upload the file. The upload will fail but the malicious script is executed.
  - [X] Affected source code:
    - [details on XSS (HackerOne)](https://hackerone.com/reports/203515)
3. **Multiple authenticated blind SQL injection (EDB-ID 40137)**
  - [X] Summary: 
    - Vulnerability types: SQLI
    - Tested in version: WordPress 4.7, Spider Video Player 1.5.16
    - Fixed in version: Spider Video Player 1.5.18
  - [X] GIF Walkthrough: 
    ![sqli-1](./sqli/sqli-1.gif)
    ![sqli-2](./sqli/sqli-2.gif)
  - [X] Steps to recreate: 
    - A logged on contributor (or higher - author, editor, or administrator) of a WordPress site (with the Spider Video Player 1.5.16 plugin installed) submits a request containing SQL statements. This [page](./sqli/index.html) can be used as example.
    - The WordPress instance responds with the data requested by the attacker.
  - [X] Affected source code:
    - [details](https://sumofpwn.nl/advisory/2016/multiple_sql_injection_vulnerabilities_in_wordpress_video_player.html)
4. **Cross-site request forgery in Insert Html Snippet plugin** 
  - [X] Summary: 
    - Vulnerability types: CSRF
    - Tested in version: WordPress 4.6, Insert Html Snippet 1.2
    - Fixed in version: Insert Html Snippet 1.2.1 
  - [X] GIF Walkthrough:
    ![csrf-1](./csrf/csrf-1.gif)
    ![csrf-2](./csrf/csrf-2.gif) 
  - [X] Steps to recreate: 
    - An administrator of a WordPress site (with the Insert HTML Snippet 1.2 plugin installed) clicks a link that leads to a malicious site.
    - The [site](./csrf/index.html), carefully crafted by an attacker, submits a POST request which changes the contents of a specific snippet kept by the plugin.
  - [X] Affected source code:
    - [plugin directory](https://plugins.trac.wordpress.org/changeset/1536764/insert-html-snippet)


## Assets

The following four files were used to carry out the attacks: 

  - [xss-comment.txt](./xss-e1/xss-comment.txt)
  - [test file\<img src=x onerror=alert(1)\>.txt](./xss-e2/test\ file\<img\ src=x\ onerror=alert(1)\>.txt)
  - [index.html](./sqli/index.html)
  - [index.html](./csrf/index.html)


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)
- [Summer of Pwnage](https://sumofpwn.nl/advisories.html)
- [WPScan vulnerability database](https://wpvulndb.com/)  

GIFs created with [GIPHY Capture](https://giphy.com/apps/giphycapture).


## Notes

The file [exploits.md](exploits.md) contains a list of all exploits I tried to recreate. I was not able to recreate the majority, fact that lead me to install plugins in order to open up the attack surface.


## License

    Copyright [2018] [Victor Alvarez Pajaro]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

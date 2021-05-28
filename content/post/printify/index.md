---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Printify.com Demo audit"
subtitle: "A well built out SEO strategy is the most cost effective way to acquire customers for your business"
summary: ""
authors: []
tags: []
categories: []
date: 2021-05-28T00:56:56+03:00
lastmod: 2021-05-28T00:56:56+03:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
{{< toc >}}

## Rank audit: printify.com rank for "custom backpacks" keyword with 13K/Mo searches has been dropped to the second position in Google SERP

{{< figure src="2.png" caption="Printify.com Rank Audit example" >}}

## Competition research: printify.com domain competitors on USA traffic

{{< figure src="3.png" caption="Printify.com Rank Audit example" >}}

## Competition research: suggesting TOP20 competitors for "merch maker" keyword on USA traffic

{{< figure src="4.png" caption="Printify.com Rank Audit example" >}}

## Competition research: checking competitor "customink.com" top pages on USA traffic

{{< figure src="5.png" caption="Printify.com Rank Audit example" >}}

## Competition/keyword research: checking keyword gap of competitor "customink.com" vs "printify.com" on USA traffic

{{< figure src="6.png" caption="Printify.com Rank Audit example" >}}

## Keyword research: sandbox example with 14K keywords to work with

{{< figure src="7.png" caption="Printify.com Rank Audit example" >}}

## Website Audit: 719 errors, 525 warnings

{{< figure src="8.png" caption="Printify.com Website Audit example" >}}

## Website Audit: website structure visualization by click depth

{{< figure src="9.png" caption="Printify.com Website Audit example" >}}

## Website Audit: website structure visualization by internal page rank

{{< figure src="10.png" caption="Printify.com Website Audit example" >}}

## Website Audit: website pages Inlink rank details

{{< figure src="11.png" caption="Printify.com Website Audit example" >}}

## Website Audit: keyword mapping to website page

{{< figure src="12.png" caption="Printify.com Website Audit example" >}}

## Website Audit: Technical audit of printify.com/custom-socks page

{{< figure src="13.png" caption="Printify.com Website Audit example" >}}

## Website Audit: Content audit of printify.com/custom-socks page

{{< figure src="14.png" caption="Printify.com Website Audit example" >}}

## Website Audit: Editing content of printify.com/custom-socks page

{{< figure src="15.png" caption="Printify.com Website Audit example" >}}

## Website Audit: TF-IDF analysis for multi-word keywords for printify.com/custom-socks

{{< figure src="16.png" caption="Printify.com Website Audit example" >}}

## Backlink profile: printify.com

{{< figure src="17-1.png" caption="Printify.com Backlink Audit example" >}}
{{< figure src="17-2.png" caption="Printify.com Backlink Audit example" >}}
{{< figure src="17-3.png" caption="Printify.com Backlink Audit example" >}}

## Backlink profile: live backlinks history

{{< figure src="18.png" caption="Printify.com Backlink Audit example" >}}

## Backlink profile: lost backlinks

{{< figure src="19.png" caption="Printify.com Backlink Audit example" >}}

## Backlink profile: domain comparison summary

{{< figure src="20.png" caption="Printify.com Backlink Audit example" >}}

## Backlink intersection: domains that all competitors, except printify.com, have backlinks from

{{< figure src="21.png" caption="Printify.com Backlink Audit example" >}}

## Security audit: Super minimal check that took just 44 seconds, but identified 3 vulnerabilities 

```bash
[root@vadimiljin ~]# docker run -it --rm wpscanteam/wpscan --url https://printify.com --enumerate u --random-user-agent
```
```txt
[+] URL: https://printify.com/ [104.22.38.205]
[+] Started: Wed May 26 12:45:55 2021

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - cf-cache-status: DYNAMIC
 |  - cf-request-id: 0a4a4ec63a00004e8cfb89c000000001
 |  - expect-ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
 |  - server: cloudflare
 |  - cf-ray: 65571a505a144e8c-FRA
 |  - alt-svc: h3-27=":443"; ma=86400, h3-28=":443"; ma=86400, h3-29=":443"; ma=86400
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: https://printify.com/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 |  - /*?*
 |  - /wp-content*
 | Found By: Robots Txt
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: https://printify.com/wp-cron.php
 | Found By: Direct Access
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.6.2 identified (Insecure, released on 2021-02-22).
 | Found By: Emoji Settings (Passive Detection)
 |  - https://printify.com/, Match: 'wp-includes\/js\/wp-emoji-release.min.js?ver=5.6.2'
 | Confirmed By: Rss Generator (Aggressive Detection)
 |  - https://printify.com/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>
 |  - https://printify.com/comments/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>
 |
 | [!] 3 vulnerabilities identified:
 |
 | [!] Title: WordPress 5.6-5.7 - Authenticated XXE Within the Media Library Affecting PHP 8
 |     Fixed in: 5.6.3
 |     References:
 |      - https://wpscan.com/vulnerability/cbbe6c17-b24e-4be4-8937-c78472a138b5
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-29447
 |      - https://wordpress.org/news/2021/04/wordpress-5-7-1-security-and-maintenance-release/
 |      - https://core.trac.wordpress.org/changeset/29378
 |      - https://blog.wpscan.com/2021/04/15/wordpress-571-security-vulnerability-release.html
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-rv47-pc52-qrhh
 |      - https://blog.sonarsource.com/wordpress-xxe-security-vulnerability/
 |      - https://hackerone.com/reports/1095645
 |      - https://www.youtube.com/watch?v=3NBxcmqCgt4
 |
 | [!] Title: WordPress 4.7-5.7 - Authenticated Password Protected Pages Exposure
 |     Fixed in: 5.6.3
 |     References:
 |      - https://wpscan.com/vulnerability/6a3ec618-c79e-4b9c-9020-86b157458ac5
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-29450
 |      - https://wordpress.org/news/2021/04/wordpress-5-7-1-security-and-maintenance-release/
 |      - https://blog.wpscan.com/2021/04/15/wordpress-571-security-vulnerability-release.html
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-pmmh-2f36-wvhq
 |      - https://core.trac.wordpress.org/changeset/50717/
 |      - https://www.youtube.com/watch?v=J2GXmxAdNWs
 |
 | [!] Title: WordPress 3.7 to 5.7.1 - Object Injection in PHPMailer
 |     Fixed in: 5.6.4
 |     References:
 |      - https://wpscan.com/vulnerability/4cd46653-4470-40ff-8aac-318bee2f998d
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-36326
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-19296
 |      - https://github.com/WordPress/WordPress/commit/267061c9595fedd321582d14c21ec9e7da2dcf62
 |      - https://wordpress.org/news/2021/05/wordpress-5-7-2-security-release/
 |      - https://github.com/PHPMailer/PHPMailer/commit/e2e07a355ee8ff36aba21d0242c5950c56e4c6f9
 |      - https://www.wordfence.com/blog/2021/05/wordpress-5-7-2-security-release-what-you-need-to-know/
 |      - https://www.youtube.com/watch?v=HaW15aMzBUM
```

Users are also identified: https://printify.com/wp-json/wp/v2/users/?per_page=100&page=1

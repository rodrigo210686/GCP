## Cloud Armor Preconfigured WAF Rules

Google Cloud Armor is Google's enterprise edge network security solution providing DDOS protection, WAF rule enforcement, and adaptive manageability at scale.

Cloud Armor has extended the preconfigured WAF rule sets to mitigate against the [OWASP Top 10](https://owasp.org/www-project-top-ten/) web application security vulnerabilities. The rule sets are based on the [OWASP Modsecurity](https://github.com/coreruleset/coreruleset/) core rule set version 3.0.2 to protect against some of the most common web application security risks including local file inclusion (lfi), remote file inclusion (rfi), remote code execution (rce), and many more.

In this lab, you learn how to mitigate some of the common vulnerabilities by using Google Cloud Armor WAF rules.

![image](https://user-images.githubusercontent.com/59710101/217625309-de8fd406-b8d8-465a-9345-b6c08de58d0f.png)


The [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) application is useful for security training and awareness, because it contains instances of each of the OWASP Top 10 security vulnerabilities—by design. An attacker can exploit it for testing purposes. In this lab, you use it to demonstrate some application attacks followed by protecting the application with Cloud Armor WAF rules. The application is fronted by a Google Cloud Load Balancer, onto which the Cloud Armor security policy and rules are be applied. It is served on the public internet thus reachable from almost anywhere and protected using Cloud Armor and VPC firewall rules.



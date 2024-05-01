# 一、系统要求
目前支持Ubuntu 20.04 LTS, Debian 10, CentOS 7/8操作系统。
CDN服务器正常运行时仅需要系统有500MB的内存。但是，程序第一次编译安装的时候需要1500MB左右的内存。若您的VPS内存不够，可以加一些Swap解决。
该程序和其他面板（比如宝塔，cPanel, Directadmin）等不兼容。

https://www.zhujizixun.com/wp-content/uploads/2020/07/atscdn.png

## 二、安装方法
一键脚本使用非常简单！只需在对应的服务器执行下面的脚本就行了。

## 1、原版（英文界面）：
```
wget https://raw.githubusercontent.com/xu5343/OneClickCDN/master/OneClickCDN.sh && sudo bash OneClickCDN.sh
```
## 2、中文版：
```
wget https://raw.githubusercontent.com/xu5343/OneClickCDN/master/translation/translated_scripts/OneClickCDN_zh-CN.sh && sudo bash OneClickCDN_zh-CN.sh
```
第一次运行时，程序会提示自动编译安装Traffic Server.  安装完毕后，程序会引导新建CDN网站，自动签发SSL等等。您需要将您网站的域名设置A记录解析到这台VPS的IP地址上。您也可以随时重新运行该脚本，用来管理您的服务器上部署的CDN网站，查看网站统计等等。

---
# OneClickCDN
A one-click shell script to set up a CDN node for your websites.

## What does this script do?
* Build Traffic Server from source.
* Add website to CDN
* Install SSL certificates
* One-click free SSL certificates from Let's Encrypt
* Manage websites, view stats, purge caches...
* Backup configurations (including SSL certificates) and restore on other nodes to quickly deploy multiple CDN nodes
* If you ever used Cloudflare, the CDN nodes created using this script will behave just like Cloudflare servers.  They will sit between clients and your origin server, caching content from the origin server, and serving your clients with content.  You can set up multiple CDN nodes by running this script on each node, and then use GeoDNS with round robin/failover to build a CDN cluster.

## System requirement
* A __freshly installed__ server, with Ubuntu 20.04 LTS 64 bit, Debian 10/11 64 bit, or CentOS 7/8 64 bit system (see notes for limitations on CentOS 7)
* __Do NOT install any web server programs (e.g., Apache, Nginx, LiteSpeed, Caddy).  Do NOT install LAMP or LEMP stack.  Do NOT install any admin panels (e.g., cPanel, DirectAdmin, BTcn, VestaCP).  They are NOT compatible with this script.__
* 1 IPv4
* At least 512 MB RAM for running CDN instance
* For the very first time, building the program from source requires about 1.5 GB RAM.  You may add SWAP to your VPS for this step.
* Root access, or sudo user

## How to use
* Firstly, you need to find a spare VPS with at least 1 IPv4, and install Ubuntu 20.04 LTS 64 bit (recommended), Debian 10 64 bit, or CentOS 7/8 64 bit OS.
* Then, please run the following command as a sudo user in SSH.
```
wget https://raw.githubusercontent.com/Har-Kuun/OneClickCDN/master/OneClickCDN.sh && sudo bash OneClickCDN.sh
```
* The script will guide you through the installation and configuration process.  You will also be prompted to add websites.
* In this process, you will be asked to set up SSL certificate.  You can choose to provide paths to your own SSL files (including private key, certificate, and CA chain certificate if applicable), or generate a free Let's Encrypt SSL certificate (not recommended, because if you have more than 1 CDN node, this will not work).  If you do choose to use the Let's Encrypt function, make sure to point your domain name to your CDN node IP BEFORE setting up the SSL.  You can always set up SSL later by selecting from the main menu.
* You can run the same script again in SSH in order to bring up the menu.  It will detect your current installation and will skip the installation process.
```
sudo bash OneClickCDN.sh
```
* If you make any changes, please make sure to exit the script by selecting the "0 - Save and quit script" option in the menu.  Changes will NOT be effective if you press Ctrl+C to quit the script.
* To uninstall the script and the Traffic Server, please run the following command in SSH.
```
wget https://raw.githubusercontent.com/Har-Kuun/OneClickCDN/master/uninstall.sh && sudo bash uninstall.sh
```


## Contact me
You can open an issue here if there is any problem/bug when you use it, or would like a new feature to be implemented.
For faster response, you can leave a message on this project webpage https://qing.su/article/oneclick-cdn.html

中文支持请访问 https://qing.su/article/oneclick-cdn.html

Thank you!

## Update log
 __Current version: v0.1.0__

|Date|Version|Changes|
|---|---|---|
|07/19/2020|v0.0.1|Script created|
|07/20/2020|v0.0.2|Add Debian 10 support; add systemd service|
|07/21/2020|v0.0.3|Add CentOS 7/8 support; add a script to uninstall Traffic Server|
|07/25/2020|v0.0.4|Add function to remove a website; fix bugs; add colored display|
|07/28/2020|v0.0.5|Add function to purge cache by URLs; fix bugs and typos|
|12/12/2021|v0.1.0|Add Debian 11 support; add backup and restore function|

## Special note
* TLS 1.3 will NOT work on CentOS 7 because of old OpenSSL version.  You can of course compile OpenSSL v1.1.1 manually, but that will potentially break a lot of other things, and is not recommended.  If TLS 1.3 is required, please consider using CentOS 8, Ubuntu 20, or Debian 10. 

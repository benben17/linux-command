<p align="center">
  <a href="https://benben17.github.io/linux-command">
    <img src="./template/img/banner.svg?sanitize=true">
  </a>
  <h1>Linux Command</h1>
</p>

[![Buy me a coffee](https://img.shields.io/badge/Buy_Me_a_Coffee-ffdd00?logo=buy-me-a-coffee&logoColor=black)](https://github.com/sponsors/benben17)
[![NPM Download](https://img.shields.io/npm/dm/linux-command.svg?style=flat)](https://www.npmjs.com/package/linux-command-en)
[![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/benben17/linux-command?logo=docker)](https://hub.docker.com/r/benben17/linux-command)

This repository collects over 600 Linux commands and is a non-profit repository. It generates a web website for easy use. Currently, the website has no ads. The content includes Linux command manuals, detailed explanations, and learning materials. The content comes from the internet and supplements from netizens. It is a very worthwhile Linux command quick reference manual to save. Copyright belongs to the original author. We do not assume any responsibility for any legal issues or risks. There is no commercial purpose. If you believe your copyright has been infringed, please let me know by email. I cannot fully guarantee the correctness of the content. Any risks arising from the use of this site's content are not my responsibility. By using this site, you accept the site's terms of use and privacy policy.

## Web Version

[Github Web](https://benben17.github.io/linux-command/) | [Githack](https://raw.githack.com/benben17/linux-command/gh-pages/index.html) | [Statically](https://cdn.statically.io/gh/benben17/linux-command/gh-pages/index.html) | [中文](https://github.com/jaywcjlove/linux-command)

Scan the QR code to preview and search on mobile, or use the link below the QR code to open and use. The following website is automatically updated thr ough Github Action.

[![Linux 命令大全](https://github.com/user-attachments/assets/5ca5c4d7-9099-4caf-b518-3b008aa26a00)](https://benben17.github.io/linux-command/)

You can freely deploy the web version, which is very simple. Just clone the [gh-pages](https://github.com/benben17/linux-command/tree/gh-pages) branch code to your static server. You can also take the Markdown files from the [`command`](https://github.com/benben17/linux-command/tree/master/command) directory and generate HTML yourself. You can also use the [Docker deployment](#docker-deployment) method below to deploy the web version.

⚠️ For the deployed static website, it's hoped that you keep a GitHub address link, so that everyone can maintain the command documentation together, making the documentation more complete and rich. Of course, if you delete all relevant information from this site, I don't really mind. By default, I allow you to do as you wish, and I don't take any responsibility. If you have also deployed a copy, you can put the link below :).

## Docker Deployment

[![Docker Image Version (latest by date)](https://img.shields.io/docker/v/benben17/linux-command?logo=docker)](https://hub.docker.com/r/benben17/linux-command) [![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/benben17/linux-command?logo=docker)](https://hub.docker.com/r/benben17/linux-command) [![Docker Pulls](https://img.shields.io/docker/pulls/benben17/linux-command?logo=docker)](https://hub.docker.com/r/benben17/linux-command)

Easily deploy the linux-command website via docker.

```bash
docker pull benben17/linux-command
```

```bash
docker run --name linux-command --rm -d -p 9665:3000 benben17/linux-command:latest
# Or
docker run --name linux-command -itd -p 9665:3000 benben17/linux-command:latest
```

Access the following URL in your browser

```bash
http://localhost:9665/
```

## Vercel

You can deploy to [Vercel](https://vercel.com) with one click using the button below:

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/benben17/linux-command)

<details>
<summary>Deploy Result</summary>

![](./assets/vercel.png)

</details>

Access through the domain assigned by Vercel, or bind your own domain in the settings.

## Netlify

You can deploy to [Netlify](https://netlify.com) with one click using the button below:

[![Deploy to Netlify Button](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/benben17/linux-command)

<details>
<summary>Deploy Result</summary>

</details>

Access through the domain assigned by Netlify, or bind your own domain in the settings.

## Baota Panel

You can quickly deploy linux-command through the Baota Panel application store

<details>
<summary>Deployment Steps</summary>

### Prerequisites

- Only applicable to Baota Panel 9.2.0 and above
- Install Baota Panel. Go to the [Baota Panel](https://www.bt.cn/new/download.html) official website, select the official version script and download to install

### Deployment

1. Log in to the Baota Panel, click `Docker` in the left menu bar
2. On first use, you will be prompted to install `Docker` and `Docker Compose` services. Click "Install Now". If already installed, ignore this step.
3. After installation, find `linux-command` in `Docker-Application Store-Utilities`, click `Install`, or search for `linux` directly in the search box.
4. Set the domain and other basic information, click `Confirm`

- Note:
  - Name: Application name, default `linuxcommand_random_characters`
  - Version selection: default `latest`
  - Domain: If you need to access via domain, please enter your domain here
  - Allow external access: If you need to access directly via `IP+Port`, check this option. If you have already set a domain, do not check this option
  - Port: Default `3000`, can be modified
  - CPU Limit: 0 means unlimited, set according to actual needs
  - Memory Limit: 0 means unlimited, set according to actual needs

5. After submission, the panel will automatically initialize the application, which takes about `1-3` minutes. You can access it after initialization is complete.

### Access linux-command

- If you have entered a domain, please enter the domain in the browser to access, such as `http://demo.linux-command`, to access the `linux-command` page.
- If you choose `IP+Port access`, please enter `http://<Baota Panel IP>:6806` in the browser address bar to access the `linux-command` page.

</details>

## 1Panel Panel

You can quickly deploy linux-command through the 1Panel application store

<details>
<summary>Deployment Steps</summary>

### Prerequisites

- Only applicable to 1Panel v1.10.32-lts and above

- Install 1Panel Panel. Go to the [1Panel](https://1panel.cn/) official website and select the official version installation script to download and install

### Deployment

1. Log in to the 1Panel panel, click `Application Store` in the left menu bar
2. Find `linux-command` in `Application Store-Development Tools`, click `Install`, or search directly in the search box
3. Click `Confirm`

- Note:
  - Name: Application name, default `linux-command`
  - Version: Default to the latest release
  - Port: Default `40255`
  - External port access: If you need to access directly via `IP+Port`, check this option, which will also open the server firewall port
  - CPU Limit: Default is 0, unlimited, can be set according to actual needs
  - Memory Limit: Default is 0, unlimited, can be set according to actual needs

4. After submission, the panel will automatically install and start the application. The application status will change to `Installing`, which takes about `1-3` minutes. Please wait patiently for installation to complete
5. When the application status changes to `Running`, click the website on the left side. On first use, you need to install `OpenResty`, click `Install`
6. After installation, click `Create` in the upper left corner of the `Website` menu bar, and select `Reverse Proxy` in the pop-up page
7. Enter your domain in the `Main Domain` field, the website code will be automatically generated. Select `http` for proxy, enter `127.0.0.1:40255` as the proxy address, and click `Confirm`
8. (Optional) Configure the website you created. You can configure `https` access as needed to enhance access security

### Access linux-command

- If you have reverse proxied the website through `OpenResty` and entered the domain, please enter the `domain` in the browser to access
- If you selected `External port access`, please enter `http://<1Panel IP>:40255` in the browser to access

</details>

## Linux Command Classification

_The Linux commands directory stored here is not complete. You can search through [linux-command](https://benben17.github.io/linux-command/). It takes the commands collected in the [command](./assets/command) directory, generates static HTML, and provides preview and index search._

### File Transfer

bye、ftp、ftpcount、ftpshut、ftpwho、ncftp、tftp、uucico、uucp、uupick、uuto、scp

### Backup and Compression

ar、bunzip2、bzip2、bzip2recover、compress、cpio、dump、gunzip、gzexe、gzip、lha、restore、tar、unarj、unzip、zip、zipinfo

### File Management

diff、diffstat、file、find、git、gitview、ln、locate、lsattr、mattrib、mc、mcopy、mdel、mdir、mktemp、mmove、mread、mren、mshowfat、mtools、mtoolstest、mv、od、paste、patch、rcp、rhmask、rm、slocate、split、tee、tmpwatch、touch、umask、whereis、which、cat、chattr、chgrp、chmod、chown、cksum、cmp、cp、cut、indent

### Disk Management

cd、df、dirs、du、edquota、eject、lndir、ls、mcd、mdeltree、mdu、mkdir、mlabel、mmd、mmount、mrd、mzip、pwd、quota、quotacheck、quotaoff、quotaon、repquota、rmdir、rmt、stat、tree、umount

### Disk Maintenance

badblocks、cfdisk、dd、e2fsck、ext2ed、fdisk、fsck.ext2、fsck、fsck.minix、fsconf、hdparm、losetup、mbadblocks、mformat、mkbootdisk、mkdosfs、mke2fs、mkfs.ext2、mkfs、mkfs.minix、mkfs.msdos、mkinitrd、mkisofs、mkswap、mpartition、sfdisk、swapoff、swapon、symlinks、sync

### System Settings

alias、apmd、aumix、bind、chkconfig、chroot、clock、crontab、declare、depmod、dircolors、dmesg、enable、eval、export、fbset、grpconv、grpunconv、hwclock、insmod、kbdconfig、lilo、liloconfig、lsmod、minfo、mkkickstart、modinfo、modprobe、mouseconfig、ntsysv、passwd、pwconv、pwunconv、rdate、resize、rmmod、rpm、set、setconsole、setenv、setup、sndconfig、SVGAText Mode、timeconfig、ulimit、unalias、unset

### System Administration

adduser、chfn、chsh、date、exit、finger、free、fwhois、gitps、groupdel、groupmod、halt、id、kill、last、lastb、login、logname、logout、logrotate、newgrp、nice、procinfo、ps、pstree、reboot、renice、rlogin、rsh、rwho、screen、shutdown、sliplogin、su、sudo、suspend、swatch、tload、top、uname、useradd、userconf、userdel、usermod、vlock、w、who、whoami、whois

### Text Processing

awk、col、colrm、comm、csplit、ed、egrep、ex、fgrep、fmt、fold、grep、ispell、jed、joe、join、look、mtype、pico、rgrep、sed、sort、spell、tr、uniq、vi、wc

### Network Communication

dip、getty、mingetty、ppp-off、smbd(samba daemon)、telnet、uulog、uustat、uux、cu、dnsconf、efax、httpd、ip、ifconfig、mesg、minicom、nc、netconf、netconfig、netstat、ping、ping6、pppstats、samba、setserial、shapecfg(shaper configuration)、smbd(samba daemon)、statserial(status ofserial port)、talk、tcpdump、testparm(test parameter)、traceroute、tty(teletypewriter)、uuname、wall(write all)、write、ytalk、arpwatch、apachectl、smbclient(samba client)、pppsetup

### Device Management

dumpkeys、loadkeys、MAKEDEV、rdev、setleds

### Email and Newsgroups

archive、ctlinnd、elm、getlist、inncheck、mail、mailconf、mailq、messages、metamail、mutt、nntpget、pine、slrn、X WINDOWS SYSTEM、reconfig、startx(start X Window)、Xconfigurator、XF86Setup、xlsatoms、xlsclients、xlsfonts

### Other Commands

yes

## Development Usage

You can install the [`linux-command`](https://www.npmjs.com/package/linux-command-en) package via `npm`, which contains markdown text for all commands and an [index file](dist/data.json).

```bash
npm install linux-command-en
```

```js
var comm = require("linux-command");
console.log("---->", comm.ls);

var alias = require("linux-command/command/alias.md");
console.log("---->", alias); // markdown string
```

You can also access the index data and corresponding command detailed content through CDN. I regularly publish new versions to provide for everyone's use. [UNPKG](https://unpkg.com/linux-command/) with version number will lock version access. Removing the version number from the request will automatically redirect to the latest version.

```shell
# Command index JSON data
https://unpkg.com/linux-command/dist/data.json
# Corresponding command details (Markdown) data
https://unpkg.com/linux-command/command/<command-name>.md
```

You can also get the latest content through Github's Raw

```shell
# Command index JSON data
https://raw.githubusercontent.com/benben17/linux-command/master/dist/data.json
# Corresponding command details (Markdown) data
https://raw.githubusercontent.com/benben17/linux-command/master/command/<command-name>.md
```

## Linux Learning Resources

### Community Websites

- [Linux China](https://linux.cn/) - Various news, articles, and technical content
- [LabEx](https://labex.io/) - Provides free online Linux environment. You can learn Linux without installing a system on your own machine. Super convenient and practical.
- [Bird's Linux Private Kitchen](http://linux.vbird.org/) - A very suitable tutorial for beginners learning Linux.
- [Linux Community](http://www.linuxidc.com/) - Has Linux-related news, tutorials, themes, and wallpapers.
- [Linux Today](http://www.linuxde.net) - Linux news and information release, Linux professional technology learning!
- [X-CMD](https://www.x-cmd.com/) - Core with Shell + AWK to enhance native command output and interactive experience. Introduction and usage tutorials for various commands and modern software packages. Daily technology news and information. Welcome to browse and follow!


### Software Tools

- [Awesome Linux Software](https://www.gitbook.com/book/alim0x/awesome-linux-software-zh_cn/details) Github Repository [Zh](https://github.com/alim0x/Awesome-Linux-Software-zh_CN) [En](https://github.com/VoLuong/Awesome-Linux-Software)

### China Open Source Mirror Sites

- Aliyun Open Source Mirror: http://mirrors.aliyun.com/
- NetEase Open Source Mirror: http://mirrors.163.com/
- Sohu Open Source Mirror: http://mirrors.sohu.com/
- Beijing Jiaotong University: http://mirror.bjtu.edu.cn/ \<Education network recommended\>
- Lanzhou University: http://mirror.lzu.edu.cn/ \<Northwest University FTP Search Engine\>
- Shanghai Jiao Tong University: http://ftp.sjtu.edu.cn/
- Tsinghua University: http://mirrors.tuna.tsinghua.edu.cn/
  - http://mirrors4.tuna.tsinghua.edu.cn/
- University of Science and Technology of China: http://mirrors.ustc.edu.cn/
  - http://ipv6.ustc.edu.cn/ \<IPv6 only\>
- Northeastern University: http://mirror.neu.edu.cn/
- Zhejiang University: http://mirrors.zju.edu.cn/
- Donsoft Information College: http://mirrors.neusoft.edu.cn/

### Gaming-Oriented Linux Distributions

_Eight best Linux distributions for gamers, organized by Open Source China. [Original article here](https://my.oschina.net/editorial-story/blog/888795)_.

- [SteamOS](http://store.steampowered.com/livingroom/SteamOS/) [Official Documentation](http://store.steampowered.com/steamos/buildyourown) [Mirror Download](http://repo.steampowered.com/download/)
- [Ubuntu GamePack](https://ualinux.com/en/ubuntu-gamepack) [Download](https://ualinux.com/en/ubuntu-gamepack)
- [Fedora – Games Spin](https://www.oschina.net/p/fedora_linux) [Download](https://labs.fedoraproject.org/en/games/)
- [SparkyLinux – GameOver Edition](https://www.oschina.net/p/sparkylinux) [Download](https://sparkylinux.org/download/#special)
- [Lakka](http://www.lakka.tv/) [Download](http://www.lakka.tv/disclaimer/)
- [Game Drift Linux](http://gamedrift.org/) [Download](http://gamedrift.org/Download.html)
- [Solus](https://solus-project.com) [Download](https://solus-project.com/download/)
- [Manjaro Gaming Edition (mGAMe)](https://sourceforge.net/projects/mgame/) [Download](https://sourceforge.net/projects/mgame/)

## Team
[![jaywcjlove](https://avatars.githubusercontent.com/u/11755695?s=100&v=4)](https://github.com/benben17)
[![jaywcjlove](https://github.com/jaywcjlove.png?size=100)](https://github.com/jaywcjlove)

## Thanks to All Contributors

As always, thanks to our outstanding contributors!

<!--AUTO_GENERATED_PLEASE_DONT_DELETE_IT-->

<a href="https://github.com/jaywcjlove" title="小弟调调"><img src="https://avatars.githubusercontent.com/u/1680273?v=4" width="42;" alt="小弟调调"/></a>
<a href="https://github.com/ZhuangZhu-74" title="ZhuangZhu-74"><img src="https://avatars.githubusercontent.com/u/49544524?v=4" width="42;" alt="ZhuangZhu-74"/></a>
<a href="https://github.com/renovate-bot" title="Mend Renovate"><img src="https://avatars.githubusercontent.com/u/25180681?v=4" width="42;" alt="Mend Renovate"/></a>
<a href="https://github.com/huckhuang" title="Huck Huang"><img src="https://avatars.githubusercontent.com/u/23023193?v=4" width="42;" alt="Huck Huang"/></a>
<a href="https://github.com/lutixiaya" title="lutixiaya"><img src="https://avatars.githubusercontent.com/u/48750425?v=4" width="42;" alt="lutixiaya"/></a>
<a href="https://github.com/le-shi" title="L"><img src="https://avatars.githubusercontent.com/u/22446162?v=4" width="42;" alt="L"/></a>
<a href="https://github.com/admxj" title="圆头圆脑"><img src="https://avatars.githubusercontent.com/u/15245021?v=4" width="42;" alt="圆头圆脑"/></a>
<a href="https://github.com/clay-wangzhi" title="clay-wangzhi"><img src="https://avatars.githubusercontent.com/u/34151437?v=4" width="42;" alt="clay-wangzhi"/></a>
<a href="https://github.com/hujingnb" title="烟草的香味"><img src="https://avatars.githubusercontent.com/u/29052630?v=4" width="42;" alt="烟草的香味"/></a>
<a href="https://github.com/gletthereblight" title="Glett"><img src="https://avatars.githubusercontent.com/u/29481184?v=4" width="42;" alt="Glett"/></a>
<a href="https://github.com/conglinyizhi" title="丛林意志"><img src="https://avatars.githubusercontent.com/u/42381347?v=4" width="42;" alt="丛林意志"/></a>
<a href="https://github.com/Jayin" title="Jayin Tang"><img src="https://avatars.githubusercontent.com/u/2763894?v=4" width="42;" alt="Jayin Tang"/></a>
<a href="https://github.com/ischenyu" title="Shan Chenyu"><img src="https://avatars.githubusercontent.com/u/103872353?v=4" width="42;" alt="Shan Chenyu"/></a>
<a href="https://github.com/lichunqiang" title="__FresHmaN"><img src="https://avatars.githubusercontent.com/u/2433916?v=4" width="42;" alt="__FresHmaN"/></a>
<a href="https://github.com/zfb132" title="Fubin Zhang"><img src="https://avatars.githubusercontent.com/u/18099238?v=4" width="42;" alt="Fubin Zhang"/></a>
<a href="https://github.com/pluveto" title="Zijing Zhang"><img src="https://avatars.githubusercontent.com/u/50045289?v=4" width="42;" alt="Zijing Zhang"/></a>
<a href="https://github.com/yibajianghudao" title="JiangHuDao"><img src="https://avatars.githubusercontent.com/u/111487502?v=4" width="42;" alt="JiangHuDao"/></a>
<a href="https://github.com/Ernest-su" title="ernest"><img src="https://avatars.githubusercontent.com/u/5917446?v=4" width="42;" alt="ernest"/></a>
<a href="https://github.com/dulltackle" title="dulltackle"><img src="https://avatars.githubusercontent.com/u/45963660?v=4" width="42;" alt="dulltackle"/></a>
<a href="https://github.com/Makonike" title="谈笑风生间"><img src="https://avatars.githubusercontent.com/u/75628309?v=4" width="42;" alt="谈笑风生间"/></a>
<a href="https://github.com/zyy2477" title="zyy2477"><img src="https://avatars.githubusercontent.com/u/23225911?v=4" width="42;" alt="zyy2477"/></a>
<a href="https://github.com/rgshare" title="rgshare"><img src="https://avatars.githubusercontent.com/u/3303320?v=4" width="42;" alt="rgshare"/></a>
<a href="https://github.com/Jeremy2214" title="Jeremy2214"><img src="https://avatars.githubusercontent.com/u/97098763?v=4" width="42;" alt="Jeremy2214"/></a>
<a href="https://github.com/MioMuse" title="MioMuse"><img src="https://avatars.githubusercontent.com/u/41938676?v=4" width="42;" alt="MioMuse"/></a>
<a href="https://github.com/SteveLauC" title="SteveLauC"><img src="https://avatars.githubusercontent.com/u/96880612?v=4" width="42;" alt="SteveLauC"/></a>
<a href="https://github.com/james-wangx" title="James Wang"><img src="https://avatars.githubusercontent.com/u/62491424?v=4" width="42;" alt="James Wang"/></a>
<a href="https://github.com/Xrtero" title="Xrtero"><img src="https://avatars.githubusercontent.com/u/55886907?v=4" width="42;" alt="Xrtero"/></a>
<a href="https://github.com/yeungchie" title="YEUNGCHIE"><img src="https://avatars.githubusercontent.com/u/30793662?v=4" width="42;" alt="YEUNGCHIE"/></a>
<a href="https://github.com/duzhuoshanwai" title="duzhuoshanwai"><img src="https://avatars.githubusercontent.com/u/65448395?v=4" width="42;" alt="duzhuoshanwai"/></a>
<a href="https://github.com/lavaicer" title="lavaicer"><img src="https://avatars.githubusercontent.com/u/52038323?v=4" width="42;" alt="lavaicer"/></a>
<a href="https://github.com/loverainye" title="loverainye"><img src="https://avatars.githubusercontent.com/u/2232094?v=4" width="42;" alt="loverainye"/></a>
<a href="https://github.com/alfchao" title="alfred"><img src="https://avatars.githubusercontent.com/u/49786895?v=4" width="42;" alt="alfred"/></a>
<a href="https://github.com/Qliangw" title="Qliangw"><img src="https://avatars.githubusercontent.com/u/22791711?v=4" width="42;" alt="Qliangw"/></a>
<a href="https://github.com/maboloshi" title="沙漠之子"><img src="https://avatars.githubusercontent.com/u/7850715?v=4" width="42;" alt="沙漠之子"/></a>
<a href="https://github.com/Evilrabbit520" title="Wang Yujia"><img src="https://avatars.githubusercontent.com/u/25611476?v=4" width="42;" alt="Wang Yujia"/></a>
<a href="https://github.com/sundakai" title="永恒"><img src="https://avatars.githubusercontent.com/u/21995250?v=4" width="42;" alt="永恒"/></a>
<a href="https://github.com/Jeffery186" title="Shell"><img src="https://avatars.githubusercontent.com/u/39795988?v=4" width="42;" alt="Shell"/></a>
<a href="https://github.com/xhal" title="H Liu"><img src="https://avatars.githubusercontent.com/u/34055638?v=4" width="42;" alt="H Liu"/></a>
<a href="https://github.com/weironz" title="will"><img src="https://avatars.githubusercontent.com/u/33590311?v=4" width="42;" alt="will"/></a>
<a href="https://github.com/Wvvatt" title="VVatt"><img src="https://avatars.githubusercontent.com/u/38394031?v=4" width="42;" alt="VVatt"/></a>
<a href="https://github.com/jcdj666" title="jcdj666"><img src="https://avatars.githubusercontent.com/u/38837009?v=4" width="42;" alt="jcdj666"/></a>
<a href="https://github.com/gggwvg" title="gggwvg"><img src="https://avatars.githubusercontent.com/u/6913118?v=4" width="42;" alt="gggwvg"/></a>
<a href="https://github.com/Dazhuangw" title="Dazhuangw"><img src="https://avatars.githubusercontent.com/u/74780009?v=4" width="42;" alt="Dazhuangw"/></a>
<a href="https://github.com/alterem" title="Alterem"><img src="https://avatars.githubusercontent.com/u/16953053?v=4" width="42;" alt="Alterem"/></a>
<a href="https://github.com/YanhiWang" title="YH"><img src="https://avatars.githubusercontent.com/u/114390595?v=4" width="42;" alt="YH"/></a>
<a href="https://github.com/XingwenZhang" title="Xingwen Zhang"><img src="https://avatars.githubusercontent.com/u/21063553?v=4" width="42;" alt="Xingwen Zhang"/></a>
<a href="https://github.com/RichardLCD" title="RichardLCD"><img src="https://avatars.githubusercontent.com/u/41584321?v=4" width="42;" alt="RichardLCD"/></a>
<a href="https://github.com/fishandsheep" title="QinShower"><img src="https://avatars.githubusercontent.com/u/43347407?v=4" width="42;" alt="QinShower"/></a>
<a href="https://github.com/hellof20" title="Pan, Wen-Ming"><img src="https://avatars.githubusercontent.com/u/8756642?v=4" width="42;" alt="Pan, Wen-Ming"/></a>
<a href="https://github.com/KrisMagical" title="KrisMagic"><img src="https://avatars.githubusercontent.com/u/144247736?v=4" width="42;" alt="KrisMagic"/></a>
<a href="https://github.com/li7355608" title="Skuld"><img src="https://avatars.githubusercontent.com/u/68886053?v=4" width="42;" alt="Skuld"/></a>
<a href="https://github.com/FunKeen" title="FunKeen"><img src="https://avatars.githubusercontent.com/u/112614943?v=4" width="42;" alt="FunKeen"/></a>
<a href="https://github.com/BingCoke" title="BingCoke"><img src="https://avatars.githubusercontent.com/u/81607010?v=4" width="42;" alt="BingCoke"/></a>
<a href="https://github.com/einverne" title="Ein Verne"><img src="https://avatars.githubusercontent.com/u/1962738?v=4" width="42;" alt="Ein Verne"/></a>
<a href="https://github.com/kmephistoh" title="kmephistoh"><img src="https://avatars.githubusercontent.com/u/2638142?v=4" width="42;" alt="kmephistoh"/></a>
<a href="https://github.com/kid1412621" title="NanoNova"><img src="https://avatars.githubusercontent.com/u/26278054?v=4" width="42;" alt="NanoNova"/></a>
<a href="https://github.com/kassadin" title="kassadin"><img src="https://avatars.githubusercontent.com/u/1104051?v=4" width="42;" alt="kassadin"/></a>
<a href="https://github.com/juemuren4449" title="juemuren4449"><img src="https://avatars.githubusercontent.com/u/12666694?v=4" width="42;" alt="juemuren4449"/></a>
<a href="https://github.com/Coder-ZJQ" title="jqz3.tech"><img src="https://avatars.githubusercontent.com/u/15013685?v=4" width="42;" alt="jqz3.tech"/></a>
<a href="https://github.com/llmons" title="illmons"><img src="https://avatars.githubusercontent.com/u/143727979?v=4" width="42;" alt="illmons"/></a>
<a href="https://github.com/hululu1068" title="hululu1068"><img src="https://avatars.githubusercontent.com/u/68652362?v=4" width="42;" alt="hululu1068"/></a>
<a href="https://github.com/leiaoo" title="leo"><img src="https://avatars.githubusercontent.com/u/8576385?v=4" width="42;" alt="leo"/></a>
<a href="https://github.com/lewis1573" title="lewis1573"><img src="https://avatars.githubusercontent.com/u/77063576?v=4" width="42;" alt="lewis1573"/></a>
<a href="https://github.com/linuxwd" title="linuxwd"><img src="https://avatars.githubusercontent.com/u/1127767?v=4" width="42;" alt="linuxwd"/></a>
<a href="https://github.com/ricardowangyf" title="Ricardowang"><img src="https://avatars.githubusercontent.com/u/81006817?v=4" width="42;" alt="Ricardowang"/></a>
<a href="https://github.com/lonlng" title="cole"><img src="https://avatars.githubusercontent.com/u/46036684?v=4" width="42;" alt="cole"/></a>
<a href="https://github.com/dufu-byte" title="dufu"><img src="https://avatars.githubusercontent.com/u/29202248?v=4" width="42;" alt="dufu"/></a>
<a href="https://github.com/miniwater" title="miniwater"><img src="https://avatars.githubusercontent.com/u/14000053?v=4" width="42;" alt="miniwater"/></a>
<a href="https://github.com/z-anshun" title="noodles2hg"><img src="https://avatars.githubusercontent.com/u/57032282?v=4" width="42;" alt="noodles2hg"/></a>
<a href="https://github.com/121812" title="Forever121"><img src="https://avatars.githubusercontent.com/u/39209748?v=4" width="42;" alt="Forever121"/></a>
<a href="https://github.com/cxalc" title="cxalc"><img src="https://avatars.githubusercontent.com/u/79086256?v=4" width="42;" alt="cxalc"/></a>
<a href="https://github.com/daydaygo" title="dayday"><img src="https://avatars.githubusercontent.com/u/3986303?v=4" width="42;" alt="dayday"/></a>
<a href="https://github.com/denymz" title="Deny"><img src="https://avatars.githubusercontent.com/u/23657601?v=4" width="42;" alt="Deny"/></a>
<a href="https://github.com/dongpohezui" title="dongpohezui"><img src="https://avatars.githubusercontent.com/u/40270581?v=4" width="42;" alt="dongpohezui"/></a>
<a href="https://github.com/ecjtusbs" title="ecjtusbs"><img src="https://avatars.githubusercontent.com/u/23614197?v=4" width="42;" alt="ecjtusbs"/></a>
<a href="https://github.com/focksor" title="focksor"><img src="https://avatars.githubusercontent.com/u/29502168?v=4" width="42;" alt="focksor"/></a>
<a href="https://github.com/mickeygo" title="gang.yang"><img src="https://avatars.githubusercontent.com/u/5130371?v=4" width="42;" alt="gang.yang"/></a>
<a href="https://github.com/hexianzhi" title="gedune"><img src="https://avatars.githubusercontent.com/u/11190425?v=4" width="42;" alt="gedune"/></a>
<a href="https://github.com/geekeryy" title="geekeryy"><img src="https://avatars.githubusercontent.com/u/12489875?v=4" width="42;" alt="geekeryy"/></a>
<a href="https://github.com/mygesty" title="gesty"><img src="https://avatars.githubusercontent.com/u/30500317?v=4" width="42;" alt="gesty"/></a>
<a href="https://github.com/gaohongy" title="ghy"><img src="https://avatars.githubusercontent.com/u/56125657?v=4" width="42;" alt="ghy"/></a>
<a href="https://github.com/githubwxz" title="githubwxz"><img src="https://avatars.githubusercontent.com/u/23112003?v=4" width="42;" alt="githubwxz"/></a>
<a href="https://github.com/hanwei1980" title="hanwei"><img src="https://avatars.githubusercontent.com/u/1889245?v=4" width="42;" alt="hanwei"/></a>
<a href="https://github.com/gcluffy" title="gcluffy"><img src="https://avatars.githubusercontent.com/u/39456622?v=4" width="42;" alt="gcluffy"/></a>
<a href="https://github.com/hotdogc1017" title="hotdogc1017"><img src="https://avatars.githubusercontent.com/u/126151508?v=4" width="42;" alt="hotdogc1017"/></a>
<a href="https://github.com/huangyoo" title="huangyao"><img src="https://avatars.githubusercontent.com/u/16477499?v=4" width="42;" alt="huangyao"/></a>
<a href="https://github.com/oliver-zch" title="oliver"><img src="https://avatars.githubusercontent.com/u/49701721?v=4" width="42;" alt="oliver"/></a>
<a href="https://github.com/lxp731" title="七朔"><img src="https://avatars.githubusercontent.com/u/95358476?v=4" width="42;" alt="七朔"/></a>
<a href="https://github.com/gclm" title="孤城落寞"><img src="https://avatars.githubusercontent.com/u/27618687?v=4" width="42;" alt="孤城落寞"/></a>
<a href="https://github.com/kindevil" title="尘埃"><img src="https://avatars.githubusercontent.com/u/846488?v=4" width="42;" alt="尘埃"/></a>
<a href="https://github.com/fseasy" title="Wei Xu"><img src="https://avatars.githubusercontent.com/u/5585818?v=4" width="42;" alt="Wei Xu"/></a>
<a href="https://github.com/yybht155" title="Loofra"><img src="https://avatars.githubusercontent.com/u/32786211?v=4" width="42;" alt="Loofra"/></a>
<a href="https://github.com/fusurus" title="扶苏如是"><img src="https://avatars.githubusercontent.com/u/57750156?v=4" width="42;" alt="扶苏如是"/></a>
<a href="https://github.com/ReZeroS" title="ReZero"><img src="https://avatars.githubusercontent.com/u/13174606?v=4" width="42;" alt="ReZero"/></a>
<a href="https://github.com/XksA-me" title="极简XksA"><img src="https://avatars.githubusercontent.com/u/43670614?v=4" width="42;" alt="极简XksA"/></a>
<a href="https://github.com/tjdxy" title="淘金的小宇"><img src="https://avatars.githubusercontent.com/u/134299557?v=4" width="42;" alt="淘金的小宇"/></a>
<a href="https://github.com/LuckyDevin" title="移动的红烧肉"><img src="https://avatars.githubusercontent.com/u/26499884?v=4" width="42;" alt="移动的红烧肉"/></a>
<a href="https://github.com/madordie" title="继刚"><img src="https://avatars.githubusercontent.com/u/10811132?v=4" width="42;" alt="继刚"/></a>
<a href="https://github.com/kapok-cjs" title="老犁"><img src="https://avatars.githubusercontent.com/u/28657624?v=4" width="42;" alt="老犁"/></a>
<a href="https://github.com/Kyofin" title="Kyofin"><img src="https://avatars.githubusercontent.com/u/18548053?v=4" width="42;" alt="Kyofin"/></a>
<a href="https://github.com/xminjie" title="谢民皆"><img src="https://avatars.githubusercontent.com/u/25931342?v=4" width="42;" alt="谢民皆"/></a>
<a href="https://github.com/fmalee" title="远方"><img src="https://avatars.githubusercontent.com/u/3209058?v=4" width="42;" alt="远方"/></a>
<a href="https://github.com/bycszzz" title="bycs"><img src="https://avatars.githubusercontent.com/u/101485931?v=4" width="42;" alt="bycs"/></a>
<a href="https://github.com/HDsky" title="Yidan Wang"><img src="https://avatars.githubusercontent.com/u/17249963?v=4" width="42;" alt="Yidan Wang"/></a>
<a href="https://github.com/rexlin600" title="rexlin600"><img src="https://avatars.githubusercontent.com/u/23032549?v=4" width="42;" alt="rexlin600"/></a>
<a href="https://github.com/sfwwslm" title="sfwwslm"><img src="https://avatars.githubusercontent.com/u/77674552?v=4" width="42;" alt="sfwwslm"/></a>
<a href="https://github.com/shhch" title="shc"><img src="https://avatars.githubusercontent.com/u/46923522?v=4" width="42;" alt="shc"/></a>
<a href="https://github.com/shuangcui" title="shuangcui"><img src="https://avatars.githubusercontent.com/u/16413463?v=4" width="42;" alt="shuangcui"/></a>
<a href="https://github.com/snovey" title="snovey"><img src="https://avatars.githubusercontent.com/u/15171147?v=4" width="42;" alt="snovey"/></a>
<a href="https://github.com/hunantangke" title="tangke"><img src="https://avatars.githubusercontent.com/u/22476435?v=4" width="42;" alt="tangke"/></a>
<a href="https://github.com/tutianyu101" title="可爱软萌喵"><img src="https://avatars.githubusercontent.com/u/134258491?v=4" width="42;" alt="可爱软萌喵"/></a>
<a href="https://github.com/UniqueDing" title="UniqueDing"><img src="https://avatars.githubusercontent.com/u/24190814?v=4" width="42;" alt="UniqueDing"/></a>
<a href="https://github.com/waiwai24" title="waiwai"><img src="https://avatars.githubusercontent.com/u/131680154?v=4" width="42;" alt="waiwai"/></a>
<a href="https://github.com/weibk" title="weibk"><img src="https://avatars.githubusercontent.com/u/79395818?v=4" width="42;" alt="weibk"/></a>
<a href="https://github.com/wlf-darkmatter" title="Lingfeng Wang"><img src="https://avatars.githubusercontent.com/u/62014693?v=4" width="42;" alt="Lingfeng Wang"/></a>
<a href="https://github.com/hkyyx" title="yanyx"><img src="https://avatars.githubusercontent.com/u/12455492?v=4" width="42;" alt="yanyx"/></a>
<a href="https://github.com/zjlovezj" title="zjlovezj"><img src="https://avatars.githubusercontent.com/u/388222?v=4" width="42;" alt="zjlovezj"/></a>
<a href="https://github.com/xin99xin" title="zodiac"><img src="https://avatars.githubusercontent.com/u/10813088?v=4" width="42;" alt="zodiac"/></a>
<a href="https://github.com/fireairforce" title="zoomdong"><img src="https://avatars.githubusercontent.com/u/32598811?v=4" width="42;" alt="zoomdong"/></a>
<a href="https://github.com/zuixin369" title="zuixin369"><img src="https://avatars.githubusercontent.com/u/54224677?v=4" width="42;" alt="zuixin369"/></a>
<a href="https://github.com/zyimm" title="zyimm"><img src="https://avatars.githubusercontent.com/u/13979159?v=4" width="42;" alt="zyimm"/></a>
<a href="https://github.com/jack-zheng" title="Jack"><img src="https://avatars.githubusercontent.com/u/5470278?v=4" width="42;" alt="Jack"/></a>
<a href="https://github.com/JackABlack" title="Jack.A.Black"><img src="https://avatars.githubusercontent.com/u/33801210?v=4" width="42;" alt="Jack.A.Black"/></a>
<a href="https://github.com/JellyObjeck" title="Jelly"><img src="https://avatars.githubusercontent.com/u/141554249?v=4" width="42;" alt="Jelly"/></a>
<a href="https://github.com/Nexchard" title="Nexchard"><img src="https://avatars.githubusercontent.com/u/61868296?v=4" width="42;" alt="Nexchard"/></a>
<a href="https://github.com/karlhorky" title="Karl Horky"><img src="https://avatars.githubusercontent.com/u/1935696?v=4" width="42;" alt="Karl Horky"/></a>
<a href="https://github.com/LaudOak" title="LaudOak"><img src="https://avatars.githubusercontent.com/u/11486158?v=4" width="42;" alt="LaudOak"/></a>
<a href="https://github.com/liux-pro" title="Legend"><img src="https://avatars.githubusercontent.com/u/20764978?v=4" width="42;" alt="Legend"/></a>
<a href="https://github.com/LexsionLee" title="LexsionLee"><img src="https://avatars.githubusercontent.com/u/10875417?v=4" width="42;" alt="LexsionLee"/></a>
<a href="https://github.com/hengliyin" title="hengli"><img src="https://avatars.githubusercontent.com/u/13692434?v=4" width="42;" alt="hengli"/></a>
<a href="https://github.com/wuxian" title="Lin Wuxian"><img src="https://avatars.githubusercontent.com/u/2416757?v=4" width="42;" alt="Lin Wuxian"/></a>
<a href="https://github.com/zlshi6" title="zlshi6"><img src="https://avatars.githubusercontent.com/u/97012545?v=4" width="42;" alt="zlshi6"/></a>
<a href="https://github.com/LesterWeng" title="Lix"><img src="https://avatars.githubusercontent.com/u/23631443?v=4" width="42;" alt="Lix"/></a>
<a href="https://github.com/LucienShui" title="Lucien"><img src="https://avatars.githubusercontent.com/u/30151093?v=4" width="42;" alt="Lucien"/></a>
<a href="https://github.com/M4n5ter" title="Wang"><img src="https://avatars.githubusercontent.com/u/68144809?v=4" width="42;" alt="Wang"/></a>
<a href="https://github.com/linmingwei" title="mwei"><img src="https://avatars.githubusercontent.com/u/20484631?v=4" width="42;" alt="mwei"/></a>
<a href="https://github.com/Marnm" title="Marnm"><img src="https://avatars.githubusercontent.com/u/13164237?v=4" width="42;" alt="Marnm"/></a>
<a href="https://github.com/XBGzZ" title="XBG"><img src="https://avatars.githubusercontent.com/u/66010822?v=4" width="42;" alt="XBG"/></a>
<a href="https://github.com/loprx" title="0x_000"><img src="https://avatars.githubusercontent.com/u/32635468?v=4" width="42;" alt="0x_000"/></a>
<a href="https://github.com/apnpc" title="AlenPann"><img src="https://avatars.githubusercontent.com/u/39884597?v=4" width="42;" alt="AlenPann"/></a>
<a href="https://github.com/Azroys" title="azroy"><img src="https://avatars.githubusercontent.com/u/73465351?v=4" width="42;" alt="azroy"/></a>
<a href="https://github.com/cy920820" title="Cui Yang"><img src="https://avatars.githubusercontent.com/u/21211512?v=4" width="42;" alt="Cui Yang"/></a>
<a href="https://github.com/DYH1319" title="DYH1319"><img src="https://avatars.githubusercontent.com/u/50073268?v=4" width="42;" alt="DYH1319"/></a>
<a href="https://github.com/DaYangtuo247" title="DaYangtuo247"><img src="https://avatars.githubusercontent.com/u/73392515?v=4" width="42;" alt="DaYangtuo247"/></a>
<a href="https://github.com/MatriXiao88" title="Danny"><img src="https://avatars.githubusercontent.com/u/13702561?v=4" width="42;" alt="Danny"/></a>
<a href="https://github.com/xyzhaocs" title="Lucas Zhao"><img src="https://avatars.githubusercontent.com/u/68425858?v=4" width="42;" alt="Lucas Zhao"/></a>
<a href="https://github.com/xyzhou-1" title="Divenire"><img src="https://avatars.githubusercontent.com/u/47747466?v=4" width="42;" alt="Divenire"/></a>
<a href="https://github.com/MarsDoge" title="Dongyan Qian"><img src="https://avatars.githubusercontent.com/u/61187351?v=4" width="42;" alt="Dongyan Qian"/></a>
<a href="https://github.com/Everything-is-one" title="Everything-is-one"><img src="https://avatars.githubusercontent.com/u/92569428?v=4" width="42;" alt="Everything-is-one"/></a>
<a href="https://github.com/tofrankie" title="Frankie"><img src="https://avatars.githubusercontent.com/u/26947203?v=4" width="42;" alt="Frankie"/></a>
<a href="https://github.com/IdiosyncraticDragon" title="Guiying Li"><img src="https://avatars.githubusercontent.com/u/3750460?v=4" width="42;" alt="Guiying Li"/></a>
<a href="https://github.com/huhuhang" title="Hang"><img src="https://avatars.githubusercontent.com/u/5147530?v=4" width="42;" alt="Hang"/></a>
<a href="https://github.com/Herbert8" title="重劍無鋒"><img src="https://avatars.githubusercontent.com/u/3112923?v=4" width="42;" alt="重劍無鋒"/></a>
<a href="https://github.com/HighScorePlayer" title="HighScorePlayer"><img src="https://avatars.githubusercontent.com/u/59147099?v=4" width="42;" alt="HighScorePlayer"/></a>
<a href="https://github.com/huntout" title="Huntout Zhang"><img src="https://avatars.githubusercontent.com/u/3908223?v=4" width="42;" alt="Huntout Zhang"/></a>
<a href="https://github.com/XD-DENG" title="Xiaodong DENG"><img src="https://avatars.githubusercontent.com/u/11539188?v=4" width="42;" alt="Xiaodong DENG"/></a>
<a href="https://github.com/Xonline-Tech" title="Xonline-Tech"><img src="https://avatars.githubusercontent.com/u/55641276?v=4" width="42;" alt="Xonline-Tech"/></a>
<a href="https://github.com/xuchunyang" title="Xu Chunyang"><img src="https://avatars.githubusercontent.com/u/4550353?v=4" width="42;" alt="Xu Chunyang"/></a>
<a href="https://github.com/yansheng836" title="Yan Sheng"><img src="https://avatars.githubusercontent.com/u/45334066?v=4" width="42;" alt="Yan Sheng"/></a>
<a href="https://github.com/liuyunbin" title="Yunbin Liu"><img src="https://avatars.githubusercontent.com/u/9609295?v=4" width="42;" alt="Yunbin Liu"/></a>
<a href="https://github.com/0Knot" title="0Knot (0KN)"><img src="https://avatars.githubusercontent.com/u/48816852?v=4" width="42;" alt="0Knot (0KN)"/></a>
<a href="https://github.com/Zlanghu" title="Zlanghu"><img src="https://avatars.githubusercontent.com/u/88917899?v=4" width="42;" alt="Zlanghu"/></a>
<a href="https://github.com/aluopy" title="One Person’s Revelry"><img src="https://avatars.githubusercontent.com/u/69625113?v=4" width="42;" alt="One Person’s Revelry"/></a>
<a href="https://github.com/amit794" title="amit794"><img src="https://avatars.githubusercontent.com/u/43886572?v=4" width="42;" alt="amit794"/></a>
<a href="https://github.com/asunrong" title="Ashine"><img src="https://avatars.githubusercontent.com/u/103101986?v=4" width="42;" alt="Ashine"/></a>
<a href="https://github.com/azureology" title="azureology"><img src="https://avatars.githubusercontent.com/u/34760051?v=4" width="42;" alt="azureology"/></a>
<a href="https://github.com/bellpk" title="bell"><img src="https://avatars.githubusercontent.com/u/12622129?v=4" width="42;" alt="bell"/></a>
<a href="https://github.com/bestlaw66" title="bestlaw66"><img src="https://avatars.githubusercontent.com/u/94432849?v=4" width="42;" alt="bestlaw66"/></a>
<a href="https://github.com/brinkqiang" title="brinkqiang"><img src="https://avatars.githubusercontent.com/u/10229072?v=4" width="42;" alt="brinkqiang"/></a>
<a href="https://github.com/c2ch" title="c2ch"><img src="https://avatars.githubusercontent.com/u/35028011?v=4" width="42;" alt="c2ch"/></a>
<a href="https://github.com/chaofanx" title="chaofan"><img src="https://avatars.githubusercontent.com/u/60053994?v=4" width="42;" alt="chaofan"/></a>
<a href="https://github.com/MinsonLee" title="MinsonLee"><img src="https://avatars.githubusercontent.com/u/22138919?v=4" width="42;" alt="MinsonLee"/></a>
<a href="https://github.com/pplmx" title="Mystic"><img src="https://avatars.githubusercontent.com/u/26994103?v=4" width="42;" alt="Mystic"/></a>
<a href="https://github.com/Zhengqbbb" title="Q.Ben Zheng"><img src="https://avatars.githubusercontent.com/u/40693636?v=4" width="42;" alt="Q.Ben Zheng"/></a>
<a href="https://github.com/rayyee" title="Ray Yee"><img src="https://avatars.githubusercontent.com/u/685149?v=4" width="42;" alt="Ray Yee"/></a>
<a href="https://github.com/wurining" title="Rining Wu"><img src="https://avatars.githubusercontent.com/u/26198634?v=4" width="42;" alt="Rining Wu"/></a>
<a href="https://github.com/robigus" title="Robigus"><img src="https://avatars.githubusercontent.com/u/8164967?v=4" width="42;" alt="Robigus"/></a>
<a href="https://github.com/RocherKong" title="Rocher"><img src="https://avatars.githubusercontent.com/u/10215178?v=4" width="42;" alt="Rocher"/></a>
<a href="https://github.com/xinshangshangxin" title="殇"><img src="https://avatars.githubusercontent.com/u/8779091?v=4" width="42;" alt="殇"/></a>
<a href="https://github.com/luoxiaohei" title="SMVirus"><img src="https://avatars.githubusercontent.com/u/7138906?v=4" width="42;" alt="SMVirus"/></a>
<a href="https://github.com/seven-steven" title="SevenSteven"><img src="https://avatars.githubusercontent.com/u/13358658?v=4" width="42;" alt="SevenSteven"/></a>
<a href="https://github.com/Azolla" title="Azolla"><img src="https://avatars.githubusercontent.com/u/65333936?v=4" width="42;" alt="Azolla"/></a>
<a href="https://github.com/roachsinai" title="RoachZhao"><img src="https://avatars.githubusercontent.com/u/9500049?v=4" width="42;" alt="RoachZhao"/></a>
<a href="https://github.com/Spaghetti-C" title="Spaghetti-C"><img src="https://avatars.githubusercontent.com/u/16163995?v=4" width="42;" alt="Spaghetti-C"/></a>
<a href="https://github.com/springsunx" title="SunX"><img src="https://avatars.githubusercontent.com/u/23657968?v=4" width="42;" alt="SunX"/></a>
<a href="https://github.com/T-TRz879" title="T-TRz879"><img src="https://avatars.githubusercontent.com/u/50860504?v=4" width="42;" alt="T-TRz879"/></a>
<a href="https://github.com/iwangjie" title="Na Meng"><img src="https://avatars.githubusercontent.com/u/23075587?v=4" width="42;" alt="Na Meng"/></a>
<a href="https://github.com/wingrez" title="Wingrez"><img src="https://avatars.githubusercontent.com/u/31106425?v=4" width="42;" alt="Wingrez"/></a>

## License

Licensed under the MIT License.

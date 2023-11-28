**使用github的Actions来编译lede固件,替代使用服务器来编译**

**方式1:**

Fork到自己的项目内点Actions，选择"编译openwrt",点击"Run workflow"，看到SSH connection to Actions输入框输入"true"然后点击Run workflow

再次点击"编译openwrt"中间出现workflow runs，选择中间的"编译openwrt",点build,等待任务进行到"Debugging with tmate"

出现"SSH: ssh xxx@xxx.tmate.io",就ssh登录xxx.tmate.io，@前面的xxx为用户名(没有密码)，登录进去后快捷键输入ctrl+c

然后输入命令```bash make menuconfig ```即可配置openwrt，配置完成后输入命令exit退出ssh，github actions会自动运行后面的编译任务


**方式2:**

先装好 Linux 系统，推荐 Debian 11 或 Ubuntu LTS,创建非root用户

更新系统克隆源代码，更新 feeds 并选择配置:

   ```bash
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
   bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
   git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
   libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
   mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pyelftools \
   libpython3-dev qemu-utils rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip \
   vim wget xmlto xxd zlib1g-dev python3-setuptools
   
   git clone https://github.com/coolsnowwolf/lede
   cd lede
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```
然后Fork到自己的项目库,把本地生成的.config配置文件和feeds.conf.default配置文件内容替换到对应的.config.bak和feeds.conf.default.bak

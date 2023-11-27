使用github的Actions来编译lede固件,替代使用服务器来编译

先Fork此项目然后本地项目下载源代码，更新 feeds 并选择配置:

   ```bash
   git clone https://github.com/coolsnowwolf/lede
   cd lede
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```
把本地生成的.config配置文件和feeds.conf.default配置文件内容替换到对应的.config.bak和feeds.conf.default.bak

找到Fork到自己的项目点Actions，选择"编译openwrt",点击"Run workflow"即可开始编译

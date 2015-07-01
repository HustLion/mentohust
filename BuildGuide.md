# Preprequisites
Thanks to (http://wangye.org/blog/archives/850/)

```
sudo apt-get install build-essential
sudo apt-get install autopoint
sudo apt-get install automake
sudo apt-get install autoconf
sudo apt-get install gettext-base gettext liblocale-gettext-perl
```

# Generate build configuration
run ` ./autogen.sh`

The result should be:

	~/mentohust$ ./autogen.sh 
	+ autopoint
	+ aclocal
	+ autoheader
	+ automake --add-missing
	+ autoconf

# Build
```
./configure
make
```
The binary will be in ./src

# Example: building for OpenWRT 14.04
```
export PATH=$PATH:/path/to/openwrt/toolchain/bin
./configure --host=mips-openwrt-linux-uclibc --disable-notify --with-pcap=/path/to/precompiled/libpcap.a
make
```




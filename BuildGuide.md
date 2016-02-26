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
Run `./autogen.sh`

The result should be:
```
~/mentohust$ ./autogen.sh
+ autopoint
+ aclocal
+ autoheader
+ automake --add-missing
+ autoconf
```

# Configure & Build
```
./configure
make
```
The binary will be in ./src

# Example
##Building for OpenWRT 14.04 @ MIPS
Suppose we have `/path/to/openwrt/toolchain/bin/mips-openwrt-linux-uclibc-gcc`

1. Building libpcap
```
cd /path/to/libpcap
export PATH=$PATH:/path/to/openwrt/toolchain/bin
./configure --host=mips-openwrt-linux-uclibc --with-pcap=linux
make
```
`libpcap.a` and `libpcap.so` will be placed in the root of libpcap directory.

2. Building libiconv (optional)
```
cd /path/to/libiconv
export PATH=$PATH:/path/to/openwrt/toolchain/bin
./configure --host=mips-openwrt-linux-uclibc --enable-static=yes --enable-shared=yes --disable-nls
make
```
`libiconv.so` and `libiconv.a` will be placed in $ROOT/lib/.libs.
If you want only static or shared library, change `--enable-static` or `--enable-shared` accordingly.

3. Building MentoHUST<br/>
Seems something is wrong with `--with-iconv-prefix`. If you want to build with libiconv, do this:
```
export PATH=$PATH:/path/to/openwrt/toolchain/bin
CFLAGS=-I/path/to/iconv/include LIBS=/path/to/iconv/lib/.libs/libiconv.a ./configure --host=mips-openwrt-linux-uclibc  --disable-arp --disable-notify --with-pcap=/path/to/pcap/libpcap.a
make
```
If you don't want to include support for libiconv, things will be much easier:
```
export PATH=$PATH:/path/to/openwrt/toolchain/bin
./configure --host=mips-openwrt-linux-uclibc --disable-nls --disable-arp --disable-notify --with-pcap=/path/to/pcap/libpcap.a
make
```

Notes:

1. ** The setup above will make the libraries statically linked.** If you want to link them dynamically, just change the `.a` prefix in library file name to `.so`.
2. Some toolchains have `libiconv.h` included but don't have a working build of `libiconv`. If you build MentoHUST with `libiconv` but Ruijie messages can not be displayed (properly), check `src/.deps/myfunc.Po` to see if a wrong header is included.


# preprequisites
Thanks to (http://wangye.org/blog/archives/850/)

'''
sudo apt-get install build-essential
sudo apt-get install autopoint
sudo apt-get install automake
sudo apt-get install autoconf
sudo apt-get install gettext-base gettext liblocale-gettext-perl
'''

## verify 
run ` ./autogen.sh`

The result should be:

	~/mentohust$ ./autogen.sh 
	+ autopoint
	+ aclocal
	+ autoheader
	+ automake --add-missing
	+ autoconf

#Build
`./configure`



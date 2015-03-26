shairport_plugin
================

ShairPort Plugin for Squeezebox Server adds airTunes support for each Squeezebox server client.

To install the plugin first install the dependancies:

    > apt-get install libcrypt-openssl-rsa-perl libio-socket-inet6-perl libwww-perl avahi-utils libio-socket-ssl-perl
    > wget http://www.inf.udec.cl/~diegocaro/rpi/libnet-sdp-perl_0.07-1_all.deb
    > dpkg -i libnet-sdp-perl_0.07-1_all.deb

Now open the LMS GUI; click on Settings, then select the Plugins tab, at the bottom of the page add the repo:

https://raw.githubusercontent.com/StuartUSA/shairport_plugin/master/public.xml

Next install the plugin and enable as per usual.

Once installed the helper app needs to be compiled and/or installed into the systems PATH. There
are a number of pre-compiled binaries in the directory:

/var/lib/squeezeboxserver/cache/InstalledPlugins/Plugins/ShairTunes/shairport_helper/pre-compiled

Copy the one for your system into the PATH, on a linux system you may copy it to:

/usr/loca/bin/shairport_helper   - note the file needs to be renamed.
 
To compile the helper app, on Linux:

    > apt-get install build-essential libssl-dev libcrypt-openssl-rsa-perl \
            libao-dev libio-socket-inet6-perl libwww-perl avahi-utils pkg-config
    > cd /var/lib/squeezeboxserver/cache/InstalledPlugins/Plugins/ShairTunes/shairport_helper/
    > make
    > cp shairport_helper /usr/local/bin
  
Lastly, ensure avahi-daemon is configured correctly. edit the file /etc/avahi/avahi-daemon.conf:

    [server]
    use-ipv4=yes
    use-ipv6=no  #if you have ios7 devices change to yes
    
    [wide-area]
    enable-wide-area=yes
    
    [publish]
    publish-aaaa-on-ipv4=no
    publish-a-on-ipv6=no
    
    [reflector]
    
    [rlimits]
    rlimit-core=0
    rlimit-data=4194304
    rlimit-fsize=0
    rlimit-nofile=300
    rlimit-stack=4194304
    rlimit-nproc=3
  
Then restart avahi-daemon and LMS to apply all settings.

See http://forums.slimdevices.com/showthread.php?100379-Announce-ShairTunes-Plugin

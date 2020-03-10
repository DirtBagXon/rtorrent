# rTorrent 0.9.6/0.13.6

    apt-get install libmaxminddb-dev build-essential libcppunit-dev automake libtool

### libtorrent

    tar -zxf libtorrent-0.13.6.tar.gz 
    cd libtorrent-0.13.6/

    patch -p1 < ../patches/lt-backport_0.9.6_algorithm_median.patch 
    patch -p1 < ../patches/lt-base-cppunit-pkgconfig.patch
    patch -p1 < ../patches/lt-open-ssl-1.1.patch
    patch -p1 < ../patches/lt-ps-better-bencode-errors_all.patch
    patch -p1 < ../patches/lt-ps-honor_system_file_allocate_all.patch
    patch -p1 < ../patches/lt-ps-log_open_file-reopen_all.patch
    patch -p0 < ../patches/client_list.cc.patch 
    patch -p1 < ../patches/tixati_peer.patch

    cat ../HACK

    export CPPFLAGS=-Wno-terminate
    ./autogen.sh 
    ./configure --with-posix-fallocate
    make -j4
    make install

### rtorrent

    tar -zxf rtorrent-0.9.6.tar.gz 
    cd rtorrent-0.9.6/

    patch -p1 < ../patches/rtorrent-mod-v3-0.9.6.patch
    patch -p1 < ../patches/rtorrent-0.9.6_vi_keybinding_tjwoosta.patch
    patch -p1 < ../patches/rt-base-cppunit-pkgconfig.patch
    patch -p1 < ../patches/geoip-rtorrent0.9.6_mmdb.patch
    patch -p1 < ../patches/lt-backport_0.9.6_algorithm_median.patch
    patch -p1 < ../patches/rt-backport_0.9.7_add_temp_filter-CH.patch

    cat ../HACK

    export CPPFLAGS=-Wno-terminate
    ./autogen.sh 
    ./configure --libdir=/usr/local/lib
    make -j4

### Misc

*Alternate patch for color - Requires .rtorrent.rc config*

    patch -p1 < ../patches/color_requires_config.patch

    # Colors: 0 = black  1 = red  
    #         2 = green  3 = yellow 
    #         4 = blue   5 = magenta 
    #         6 = cyan   7 = white

    color_active_fg   = 1
    color_inactive_fg = 3
    color_dead_fg     = 1
    color_finished_fg = 2
    color_active_bg   = 2
    color_inactive_bg = 0
    color_dead_bg     = 0
    color_finished_bg = 0

### Docs

https://wiki.theory.org/BitTorrentSpecification#peer_id

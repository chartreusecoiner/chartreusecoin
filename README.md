# Install Prerequisites

Using MacPorts (or HomeBrew, but these instructions will assume MacPorts), install the required libraries.

    sudo port install boost db48 openssl miniupnpc qrencode qt4-mac

**Important**: The makefile and QT project file assume a build for a 32-bit target for maximum compatibility. Edit /opt/local/etc/macports/macports.conf and uncomment "build_arch i386". It is possible to have a second 32-bit install just for these builds.

**Also Important**: The current version of boost (1.53 at time of writing) does not work with i386 builds. You will need to install 1.47.0 from MacPorts svn (svn co --revision 85591 http://svn.macports.org/repository/macports/trunk/dports/devel/boost). See https://trac.macports.org/wiki/howto/InstallingOlderPort for details.

# Building chartreusecoind

    cd src
    make -f makefile.osx RELEASE=true

# Building Chartreusecoin-Qt
With the prerequisite software installed, do the following:

    qmake RELEASE=1 USE_UPNP=1 USE_QRCODE=1 bitcoin-qt.pro
    make
    export QTDIR=/opt/local/share/qt4
    T=$(contrib/qt_translations.py $QTDIR/translations src/qt/locale)
    python2.7 contrib/macdeploy/macdeployqtplus  -add-qt-tr $T -dmg -fancy contrib/macdeploy/fancy.plist chartreusecoin-Qt.app

After this step, you should find Chartreusecoin-Qt.dmg in your working directory.

# ChartreuseCoin (CHA)

ChartreuseCoin is an innovative, secure and energy efficient PoW/PoS coin that is better than BlueCoin. It uses a faster PoW distribution mechanism to distribute the initial coins, then after 100 days the coin is basically transferred to a pure PoS coin, where the generation of the coin is mainly through the PoS interests or something.




FROM centos:7
MAINTAINER Justin Bard <jbard@justbard.com>

RUN yum -y install wget unzip glibc.i686 compat-libstdc++-33-3.2.3-72.el7.i686 bzip2 && \
    wget http://justbard.com/assets/DedicatedServer3339-BonusPack.zip && \
    mkdir -p /usr/src/ut2004 && \
    unzip DedicatedServer3339-BonusPack.zip -d /usr/src/ut2004 && \
    rm -f DedicatedServer3339-BonusPack.zip && \
    # Fix broken CSS
    # See: http://forums.tripwireinteractive.com/showpost.php?p=585435&postcount=13
    sed -i 's/none}/none;/g' "/usr/src/ut2004/Web/ServerAdmin/ut2003.css" && \
    sed -i 's/underline}/underline;/g' "/usr/src/ut2004/Web/ServerAdmin/ut2003.css" && \
    wget http://justbard.com/assets/ut2004-lnxpatch3369-2.tar.bz2 && \
    tar -xvjf ut2004-lnxpatch3369-2.tar.bz2 -C /usr/src/ut2004 UT2004-Patch/ --strip-components=1 && \
    rm -f ut2004-lnxpatch3369-2.tar.bz2 && \
    chmod +x /usr/src/ut2004/System/ucc-bin && \
    rm -f /usr/src/ut2004/System/UT2004.ini && \
    yum clean all

COPY UT2004.ini /usr/src/ut2004/System/
WORKDIR /usr/src/ut2004/System
ENV PATH=$PATH:/usr/src/ut2004/System

EXPOSE 7777/udp 7778/udp 7787/udp 28902 8088

CMD ["ucc-bin", "server", "CTF-BridgeOfFate?game=XGame.xCTFGame", "ini=UT2004.ini", "-nohomedir"]

FROM ubuntu:16.04
LABEL maintainer="kmdgeek"

ENV OCSERV_VER 0.11.10
ENV DEPENDS wget build-essential iptables libgnutls28-dev libev-dev \
    libwrap0-dev libpam0g-dev liblz4-dev libseccomp-dev libreadline-dev \
    libnl-route-3-dev libkrb5-dev liboath-dev libradcli-dev \
    libprotobuf-c0-dev libtalloc-dev libhttp-parser-dev libpcl1-dev \
    libopts25-dev autogen protobuf-c-compiler gperf liblockfile-bin nuttcp \
    lcov libuid-wrapper libnss-wrapper libsocket-wrapper gss-ntlmssp libpam-oath

ADD run.sh /
WORKDIR /tmp
RUN chmod +x /run.sh \
 && apt-get update && apt-get upgrade -y && apt-get install -y ${DEPENDS} \
 && wget ftp://ftp.infradead.org/pub/ocserv/ocserv-${OCSERV_VER}.tar.xz \
 && tar xvf ocserv-*.tar.xz \
 && cd ocserv-* \
 && ./configure --enable-code-coverage \
 && make \
 && make check \
 && make code-coverage-capture \
 && make install \
 && cd .. \
 && rm -rf /tmp/* \
 && apt-get autoremove -y \
 && apt-get clean -y

CMD ["/run.sh"]

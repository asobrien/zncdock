FROM gliderlabs/alpine:3.3

MAINTAINER "Anthony O."

# build dependencies
RUN apk add --no-cache \
        autoconf \
        automake \
        gettext-dev \
        g++ \
        git \
        icu-dev \
        make \
        openssl-dev \
        pkgconfig \
        zlib-dev

RUN adduser -h /home/znc -D znc znc \
    && mkdir -p /build \
    && chown znc:znc /build

USER znc

# Build it
WORKDIR /build

RUN curl -L -O http://znc.in/releases/znc-1.6.2.tar.gz \
    && tar -xzvf znc*.*gz \
    && cd znc* \
    && ./configure --prefix="/home/znc" \
    && make \
    && make install

# WORKDIR /root/znc/bin
# # Build modules
# # see: http://wiki.znc.in/Compiling_modules#Installing_a_module
# RUN ./znc-buildmod /build/znc-1.6.2/modules/webadmin.cpp \
#     && ./znc-buildmod /build/znc-1.6.2/modules/webadmin.cpp

VOLUME /share

# RUN echo "DONE!"

# Share it
CMD cd /home/znc \
    && tar -zcvf /share/znc-build-1.6.2.tar.gz /home/znc

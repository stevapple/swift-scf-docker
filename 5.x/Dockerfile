FROM centos:7.6.1810
LABEL maintainer="YR Chen <stevapple@icloud.com>"
LABEL description="Docker Container for Swift with Tencent SCF Custom Runtime"

RUN yum install centos-release-scl-rh -y \
    && yum clean all -y

RUN yum install shadow-utils -y \
      binutils \
      gcc \
      glibc-static \
      libbsd-devel \
      libcurl-devel \
      libedit-devel \
      libicu-devel \
      libstdc++-static \
      libxml2-devel \
      pkg-config \
      python3 \
      sqlite \
      zlib-devel \
      zip \
    && yum clean all -y

RUN yum install rh-git227-git -y \
    && yum clean all -y

RUN echo "source /opt/rh/rh-git227/enable" >> /etc/profile.d/sh.local
ENV ENV=/etc/profile.d/sh.local

RUN sed -i -e 's/\*__block/\*__libc_block/g' /usr/include/unistd.h

# Everything up to here should cache nicely between Swift versions, assuming dev dependencies change little

# pub   4096R/ED3D1561 2019-03-22 [expires: 2021-03-21]
#       Key fingerprint = A62A E125 BBBF BB96 A6E0  42EC 925C C1CC ED3D 1561
# uid                  Swift 5.x Release Signing Key <swift-infrastructure@swift.org
ARG SWIFT_SIGNING_KEY=A62AE125BBBFBB96A6E042EC925CC1CCED3D1561
ARG SWIFT_PLATFORM=centos7
ARG SWIFT_BRANCH=swift-#SWIFT_VERSION#-release
ARG SWIFT_VERSION=swift-#SWIFT_VERSION#-RELEASE
ARG SWIFT_WEBROOT=https://download.swift.org

ENV SWIFT_SIGNING_KEY=$SWIFT_SIGNING_KEY \
    SWIFT_PLATFORM=$SWIFT_PLATFORM \
    SWIFT_BRANCH=$SWIFT_BRANCH \
    SWIFT_VERSION=$SWIFT_VERSION \
    SWIFT_WEBROOT=$SWIFT_WEBROOT

RUN set -e; \
    SWIFT_WEBDIR="$SWIFT_WEBROOT/$SWIFT_BRANCH/$(echo $SWIFT_PLATFORM | tr -d .)" \
    && SWIFT_BIN_URL="$SWIFT_WEBDIR/$SWIFT_VERSION/$SWIFT_VERSION-$SWIFT_PLATFORM.tar.gz" \
    && SWIFT_SIG_URL="$SWIFT_BIN_URL.sig" \
    # - Download the GPG keys, Swift toolchain, and toolchain signature, and verify.
    && export GNUPGHOME="$(mktemp -d)" \
    && curl -fsSL "$SWIFT_BIN_URL" -o swift.tar.gz "$SWIFT_SIG_URL" -o swift.tar.gz.sig \
    && gpg --batch --quiet --keyserver keyserver.ubuntu.com --recv-keys "$SWIFT_SIGNING_KEY" \
    && gpg --batch --verify swift.tar.gz.sig swift.tar.gz \
    # - Unpack the toolchain, set libs permissions, and clean up.
    && tar -xzf swift.tar.gz --directory / --strip-components=1 \
    && chmod -R o+r /usr/lib/swift \
    && rm -rf "$GNUPGHOME" swift.tar.gz.sig swift.tar.gz

# Print Installed Swift Version
RUN swift --version

FROM centos:7.6.1810
LABEL maintainer="YR Chen <stevapple@icloud.com>"
LABEL description="Docker Container for Swift with Tencent SCF Custom Runtime (Alpha)"

# Install newer git and gcc
RUN yum install epel-release centos-release-scl-rh -y \
    && yum install rh-git227-git -y \
    && yum clean all -y

# Enable scl installation
RUN echo "source /opt/rh/rh-git227/enable" >> /etc/profile.d/sh.local
ENV ENV=/etc/profile.d/sh.local

# Install swiftlang
RUN curl https://download.swift.org/experimental-use-only/repo/centos/releases/7/swiftlang.repo > /etc/yum.repos.d/swiftlang.repo \
    && yum install swiftlang -y \
    && yum clean all -y

# Print Installed Swift Version
RUN swift --version

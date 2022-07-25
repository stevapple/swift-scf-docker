FROM centos:7.6.1810
LABEL maintainer="YR Chen <stevapple@icloud.com>"
LABEL description="Docker Container for Swift with Tencent SCF Custom Runtime (Alpha)"

# Install newer git and gcc
RUN yum install epel-release centos-release-scl-rh -y \
    && yum install rh-git227-git devtoolset-11-gcc-c++ -y \
    && yum clean all -y

# Install swiftlang
RUN curl https://download.swift.org/experimental-use-only/repo/centos/releases/7/swiftlang.repo > /etc/yum.repos.d/swiftlang.repo \
    && yum install swiftlang -y \
    && yum clean all -y

# Print Installed Swift Version
RUN swift --version

# Activate SCl installation
COPY --chown=root:root swift-scf.sh /etc/profile.d/
ENV ENV=/etc/profile.d/swift-scf.sh

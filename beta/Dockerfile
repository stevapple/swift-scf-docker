FROM centos:7.7.1908
LABEL maintainer="YR Chen <stevapple@icloud.com>"
LABEL description="Docker Container for Swift with Tencent SCF Custom Runtime (Beta)"

# Install git 2.24
RUN yum install https://repo.ius.io/ius-release-el7.rpm -y \
    && yum install git224 -y \
    && yum clean all -y

# Install swiftlang
RUN curl https://download.swift.org/test-rpm/repo/centos/releases/7/swiftlang.repo > /etc/yum.repos.d/swiftlang.repo \
    && yum install swiftlang -y \
    && yum clean all -y

# Print Installed Swift Version
RUN swift --version

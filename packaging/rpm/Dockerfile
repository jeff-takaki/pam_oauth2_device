FROM centos:7

RUN yum install -y \
    gcc \
    gcc-c++ \
    libcurl-devel \
    make \
    openldap-devel \
    pam-devel \
    rpm-build \
 && yum clean all

RUN groupadd runner \
 && useradd --create-home --gid runner runner

USER runner

# This version must be identical to the version in pamoauth2device.spec
ENV PACKAGE_VERSION=0.1

WORKDIR /home/runner

RUN mkdir -p rpmbuild/SOURCES \
 && cd rpmbuild/SOURCES \
 && curl -L -O https://github.com/stfc/pam_oauth2_device/archive/v${PACKAGE_VERSION}.tar.gz

COPY pamoauth2device.spec .

USER root

RUN chown runner:runner pamoauth2device.spec

USER runner

RUN rpmbuild -ba pamoauth2device.spec

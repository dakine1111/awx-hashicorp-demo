FROM registry.redhat.io/ansible-automation-platform-23/ee-supported-rhel8:latest
RUN rpm -ivh https://cdn-ubi.redhat.com/content/public/ubi/dist/ubi8/8/x86_64/baseos/os/Packages/w/which-2.21-18.el8.x86_64.rpm
RUN rpm -ivh https://cdn-ubi.redhat.com/content/public/ubi/dist/ubi8/8/x86_64/baseos/os/Packages/o/openssl-1.1.1k-9.el8_7.x86_64.rpm
RUN pip3 install --no-cache-dir hvac

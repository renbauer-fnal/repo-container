FROM centos:8

RUN cat /etc/resolv.conf

RUN yum install -y createrepo rpm-build rpm-sign python3

WORKDIR /root/repo

ADD packages packages
ADD specs specs

RUN mkdir -m600 keys

ENV GNUPGHOME="keys"

RUN gpg --no-tty --batch --gen-key specs/repo-pgp-key.batch

RUN gpg --armor --export my-repo-key > pgp-key.public

# RUN gpg --armor --export-secret-keys my-repo-key | gpg --import

RUN rpm --define "_gpg_name my-repo-key" --addsign packages/*.rpm

RUN createrepo packages

RUN gpg --detach-sign --armor packages/repodata/repomd.xml

EXPOSE 8000

CMD python3 -m http.server  8000

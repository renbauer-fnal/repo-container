FROM centos:8

WORKDIR /root/repo

ADD packages packages
ADD specs specs

RUN yum install -y createrepo rpm-build rpm-sign python3

RUN mkdir keys

ENV GNUPGHOME="$(mktemp -d keys/pgpkeys-XXXXXX)"

RUN gpg --no-tty --batch --gen-key specs/repo-pgp-key.batch

RUN gpg --armor --export my-repo-key > pgp-key.public

RUN rpm --addsign packages/*.rpm

RUN pushd packages

RUN yum install -y createrepo

RUN createrepo .

RUN gpg --detach-sign --armor repodata/repomd.xml

RUN popd

ENTRYPOINT python3 -m http.server

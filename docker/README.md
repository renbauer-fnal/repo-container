Place packages in packages/directory, then:

1) docker build . -t easyrepo
2) docker run -it -p 8000:8000 easyrepo:latest

elsewhere, run:

1) yum-config-manager --add-repo &lt;hostaddress&gt;:8000/specs/easyrepo.repo
2) yum install &lt;packages&gt;

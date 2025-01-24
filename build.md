To build locally based on [issue #12226](https://github.com/kubernetes/ingress-nginx/issues/12226):

The dockerfile:

```dockerfile
FROM golang:1.23.5-alpine3.21 AS build

RUN apk update && apk add curl git vim wget && \
    mkdir -p /app/goreleaser && \
    cd /app/goreleaser && \
    wget https://github.com/goreleaser/goreleaser/releases/download/v2.6.1/goreleaser_Linux_x86_64.tar.gz && \
    tar zxf goreleaser_Linux_x86_64.tar.gz && \
    mv goreleaser /bin/goreleaser && \
    cd /app && \
    git clone https://github.com/kubernetes/ingress-nginx && \
    cd ingress-nginx
```

Then run 

```bash
docker run --rm -it golang:1.23.5-alpine3.21
docker build -t manios:ingressnginx .
docker run --rm -it manios:ingressnginx

git config --global user.email "maniopaido@gmail.com"
git config --global user.name "Christos Manios"
nginxversion="1.12.0" && \
git checkout -b "releasev${nginxversion}" "refs/tags/controller-v${nginxversion}" && \
rm -f -r dist/ "v${nginxversion}/" && \
sed -i -e '1i\version: 2' -e "/project_name: ingress-nginx/a\snapshot:\n  version_template: \"{{ .Tag }}-dirty\"" .goreleaser.yaml && \
git tag -a v${nginxversion} -m "Custom build v${nginxversion}" && \
goreleaser release --snapshot --clean && \
mkdir v${nginxversion}/ && \
mv dist/*.tar.gz "v${nginxversion}/" && \
git checkout .
```
# melange-php-demos
PHP demos for Melange + Apko

```
rm *.rsa *.pub *.tar *.cdx
rm sbom*.json
rm -rf packages

docker run --rm -v "${PWD}":/work cgr.dev/chainguard/melange keygen

docker run --privileged --rm -v "${PWD}":/work \
cgr.dev/chainguard/melange build melange.yaml \
--arch amd64 --signing-key melange.rsa

docker run --rm --workdir /work -v ${PWD}:/work \
cgr.dev/chainguard/apko build apko.yaml hello-minicli:test \
hello-minicli.tar --arch host

docker rmi hello-minicli:test-amd64
docker load < hello-minicli.tar
docker run --rm hello-minicli:test-amd64
```

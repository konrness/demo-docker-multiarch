= demo-docker-multiarch =

https://www.docker.com/blog/multi-platform-docker-builds/

https://hub.docker.com/r/konrness/arch-test

docker buildx build -t local-build .
docker run --rm local-build
docker buildx build --platform linux/arm/v7 -t arm-build .
docker run --rm arm-build

docker buildx build --platform linux/arm/v7 -t konrness/arch-test:armv7 .
docker push konrness/arch-test:armv7
docker buildx build -t konrness/arch-test:amd64 .
docker push konrness/arch-test:amd64

docker manifest create konrness/arch-test:multi konrness/arch-test:amd64 konrness/arch-test:armv7
docker manifest push konrness/arch-test:multi
docker run konrness/arch-test:multi

docker manifest inspect --verbose konrness/arch-test:multi

https://www.docker.com/blog/multi-arch-build-and-images-the-simple-way/

docker buildx create --use
docker buildx build --push --platform linux/arm/v7,linux/arm64/v8,linux/amd64 --tag konrness/arch-test:buildx-multi .



NEXT:

https://github.com/containers/buildah/issues/1590
https://hub.docker.com/r/maniator/dind-buildx
https://github.com/docker-library/docker/issues/313
https://github.com/docker/build-push-action/issues/302

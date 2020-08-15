# swift-scf-docker

Forked from [apple/swift-docker](https://github.com/apple/swift-docker), modified for [Tencent Cloud SCF](https://cloud.tencent.com/product/scf).

### Docker images for [Swift](https://swift.org) on [SCF Custom Runtime](https://cloud.tencent.com/document/product/583/47274).

#### You can find the Docker Hub repo here: [https://hub.docker.com/r/stevapple/swift-scf](https://hub.docker.com/r/stevapple/swift-scf)

### Usage

##### Pull the Docker image from Docker Hub:

```bash
docker pull stevapple/swift-scf:nightly
```

##### Create a container from the image and run it:

```bash
docker run -it stevapple/swift-scf:5.2.5 /bin/bash
```

If you want to run the Swift REPL you will need to run the container with additional privileges:

```bash
docker run --security-opt seccomp=unconfined -it stevapple/swift-scf:5.2.5
```

## Contributions

Contributions via pull requests are welcome and encouraged :)

## License

swift-scf-docker is licensed under the [Apache License, Version 2.0](LICENSE).

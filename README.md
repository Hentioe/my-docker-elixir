# my-docker-elixir

A list of Elixir images maintained by me that are automatically built and pushed to [Docker Hub](https://hub.docker.com/repository/docker/hentioe/elixir).

## Introduction

This series of images is a new choice in addition to the official images. All of Hentioe's own projects are based on this series of images.

## Version

This repository typically maintains only the latest two minor versions, such as the current `1.15` and `1.14`. It is built on top of the base images needed by Hentioe, mainly Debian (`-slim`) and Alpine (`-alpine`).

>Due to Docker Hub's limitations on the use of automatic build features, the images in this repository are built and pushed from a CI server.

## Usage

Pull the latest image:

```bash
docker pull hentioe/elixir:1.15-otp-26-slim
```

You can also pull without specifying any tags, which will default to fetching the latest version, including release candidate (RC) versions. Additionally, you can use image tags with specific revision numbers, such as `1.15.6-otp-26-slim`.

## Supported tags and respective `Dockerfile` links

- [`1.15.6-otp-26-slim`, `1.15-otp-26-slim`, `latest`](https://github.com/Hentioe/my-docker-elixir/blob/main/1.15/otp-26-slim/Dockerfile)
- [`1.15.6-otp-26-alpine`, `1.15-otp-26-alpine`](https://github.com/Hentioe/my-docker-elixir/blob/main/1.15/otp-26-alpine/Dockerfile)
- [`1.14.5-otp-26-slim`, `1.14-otp-26-slim`](https://github.com/Hentioe/my-docker-elixir/blob/main/1.14/otp-26-slim/Dockerfile)
- [`1.14.5-otp-26-alpine`, `1.14-otp-26-alpine`](https://github.com/Hentioe/my-docker-elixir/blob/main/1.14/otp-26-alpine/Dockerfile)

## Local build

To pull this project to your local machine and execute the `build.exs` script to quickly build and test the required image.

Command Syntax: `elixir build.exs [version] [base]`, where `[version]` represents the complete Elixir version, and `[base]` represents the base image.

_The `[version]` parameter must include the `patch` version number._

Example: Build an image with Elixir version `1.15.6` based on `otp-26-slim`:

```bash
elixir build.exs 1.15.6 otp-26-slim
```

If the last line of the output shows `ok` it indicates a successful build and test. The resulting image will be named `local/elixir:1.15-otp-26-slim`.

_Note: The label of the completed local image does not include the `patch` version number._

## Advantages

1. Typically, the versions of images in this repository are updated more quickly because the official image maintainers are slow.
2. This repository is based on Erlang images I build myself. Similarly, these Erlang image versions are updated more quickly. Importantly, the images in this repository are based on more specific Erlang versions, such as `26.0` rather than just `26`.

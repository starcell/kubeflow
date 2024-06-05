### jupyter-pytorch-cuda-full 이미지에 sudo 기능 추가
### -by npark, 2024/06/04

#
# This Makefile is templated, the following targets are provided:
#  - Current Architecture:
#     - docker-build:     build the docker image
#     - docker-build-dep: build the docker image (and any base images)
#     - docker-push:      push the docker image
#     - docker-push-dep:  push the docker image (and any base images)
#  - Multi-Architecture:
#     - docker-build-multi-arch:          build the docker image
#     - docker-build-multi-arch-dep:      build the docker image (and any base images)
#     - docker-build-push-multi-arch:     build AND push the docker image
#     - docker-build-push-multi-arch-dep: build AND push the docker image (and any base images)
#

GIT_COMMIT     := $(shell git rev-parse HEAD)
GIT_TREE_STATE := $(shell test -n "`git status --porcelain`" && echo "-dirty" || echo "")

BASE_REGISTRY ?= docker.io/kubeflownotebookswg
REGISTRY ?= starcell.net/kubeflownotebookdck
TAG      ?= sha-$(GIT_COMMIT)$(GIT_TREE_STATE)

IMAGE_NAME := jupyter-pytorch-cuda-full-sudo

# BASE_IMAGE         := $(REGISTRY)/jupyter-pytorch-cuda-full:$(TAG)
BASE_IMAGE         := $(BASE_REGISTRY)/jupyter-pytorch-cuda-full:$(TAG)
BASE_IMAGE_FOLDERS := jupyter-pytorch-cuda-full

# we use a separate registry-type cache to keep the main registry clean
# https://docs.docker.com/build/cache/backends/
CACHE_IMAGE ?= ghcr.io/kubeflow/kubeflow/notebook-servers/build-cache
CACHE_TAG   ?= $(IMAGE_NAME)

# https://docs.docker.com/engine/reference/commandline/buildx_build/#platform
ARCH ?= linux/amd64

# include build targets from common
include ../common.mk
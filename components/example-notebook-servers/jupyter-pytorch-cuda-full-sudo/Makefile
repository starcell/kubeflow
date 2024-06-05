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
# ex cli) 
#		make docker-build
#		make docker-push
# make 설치 : 
# 	sudo apt update
#		sudo apt install make

# GIT_COMMIT     := $(shell git rev-parse HEAD)
# sha-0b7e3d5fe5f0daeac9a6605008a77ee184829187
# git hub를 포크해서 사용하므로 위 방식으로 하면 실제 저장소에 없는 값으로 찾게됨
# docker hub에서 tag 값을 직접 복사해서 사용
# https://hub.docker.com/r/kubeflownotebookswg/jupyter-pytorch-cuda-full/tags
GIT_COMMIT     := 51606c6f476d9ee19b610872fa6e84ab04679ad9
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

# push images in this folder
.PHONY: dck-push
docker-push:
	@echo "\n\n"
	@echo "------------------------------------------------------------------------------"
	@echo "Pushing '$(IMAGE_NAME)' image..."
	@echo "tag name '$(TAG_NAMES)' ..."
	@echo "------------------------------------------------------------------------------"
	@echo ""
	docker tag $(IMAGE_NAME) $(REGISTRY)/$(IMAGE_NAME)
	docker push $(TAG_NAMES)
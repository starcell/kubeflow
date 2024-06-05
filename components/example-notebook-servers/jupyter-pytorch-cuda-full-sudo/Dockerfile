#
# NOTE: Use the Makefiles to build this image correctly.
#

ARG BASE_IMG=<jupyter-pytorch-cuda-full>
FROM $BASE_IMG

# sudo 사용을 가능하게 설정, password는 없음
USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
          sudo \
          apt-utils \
  && usermod -aG sudo ${NB_USER} \
  && echo ${NB_USER}:${NB_USER} | chpasswd \
  && echo "${NB_USER} ALL=(root) NOPASSWD:SETENV: /init" >> /etc/sudoers

USER jovyan

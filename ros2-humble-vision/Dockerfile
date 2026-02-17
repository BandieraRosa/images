# syntax=docker/dockerfile:1.6

FROM ros:humble-ros-base-jammy

ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-lc"]

ARG VISION_REPO_SSH="git@github.com:BandieraRosa/vision_dev.git"
ARG VISION_BRANCH=""

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    openssh-client \
    ca-certificates \
    curl \
    unzip \
    build-essential \
    cmake \
    ninja-build \
    python3-pip \
    python3-rosdep \
    python3-colcon-common-extensions \
    libwpa-client-dev \
    libnm-dev \
    libudev-dev \
    libasio-dev \
    && rm -rf /var/lib/apt/lists/*

RUN rosdep init || true

RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh && \
    ssh-keyscan github.com >> /root/.ssh/known_hosts && \
    chmod 644 /root/.ssh/known_hosts


WORKDIR /opt/ws
RUN --mount=type=ssh \
    set -euxo pipefail; \
    if [[ -n "${VISION_BRANCH}" ]]; then \
      git clone --recursive --branch "${VISION_BRANCH}" "${VISION_REPO_SSH}" vision_dev; \
    else \
      git clone --recursive "${VISION_REPO_SSH}" vision_dev; \
    fi

WORKDIR /opt/ws/vision_dev
RUN set -euxo pipefail; \
    source /opt/ros/humble/setup.bash; \
    rosdep update; \
    rosdep install --from-paths src --ignore-src -r -y


ENV DEBIAN_FRONTEND=dialog
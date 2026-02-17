FROM ros:humble-ros-base-jammy

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-colcon-common-extensions \
    python3-rosdep \
    build-essential \
    cmake \
    ninja-build \
    libwpa-client-dev libnm-dev libudev-dev libasio-dev \
    git ca-certificates curl \
  && rm -rf /var/lib/apt/lists/*

RUN rosdep init || true
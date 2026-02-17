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
    unzip

RUN rosdep init || true

RUN git clone https://github.com/BandieraRosa/vision_dev.git --recursive && \
    cd vision_dev && \
    source /opt/ros/humble/setup.bash && \
    rosdep install --from-paths src --ignore-src -r -y \
    && rm -rf /var/lib/apt/lists/*


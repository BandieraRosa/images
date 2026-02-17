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
    unzip \
    openssh-client \
    && rm -rf /var/lib/apt/lists/*

RUN rosdep init || true

RUN mkdir -p /root/.ssh && \
    chmod 700 /root/.ssh && \
    ssh-keyscan github.com >> /root/.ssh/known_hosts && \
    chmod 644 /root/.ssh/known_hosts

RUN git clone --recursive git@github.com:BandieraRosa/vision_dev.git && \
    cd vision_dev && \
    source /opt/ros/humble/setup.bash && \
    rosdep install --from-paths src --ignore-src -r -y

RUN rm -rf /root/.ssh/*

ENV DEBIAN_FRONTEND=dialog
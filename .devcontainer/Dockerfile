FROM osrf/ros:humble-desktop-full

ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user and ensure the default shell is /bin/bash
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install basic development tools and extra ROS 2 tools
# Included: PlotJuggler and Foxglove Bridge
RUN apt-get update && apt-get install -y \
    python3-pip \
    git \
    bash-completion \
    ros-humble-plotjuggler-ros \
    ros-humble-foxglove-bridge \
    && rm -rf /var/lib/apt/lists/*

# Source ROS 2 setup automatically in .bashrc
RUN echo "source /opt/ros/humble/setup.bash" >> /home/$USERNAME/.bashrc

USER $USERNAME
CMD ["/bin/bash"]
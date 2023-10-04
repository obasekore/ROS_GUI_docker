FROM ubuntu:18.04

# install xpra
ARG DEBIAN_FRONTEND=noninteractive
RUN apt update -y && \
    apt install -y wget ca-certificates

RUN wget -O "/usr/share/keyrings/xpra.asc" https://xpra.org/xpra.asc
RUN cd /etc/apt/sources.list.d && wget https://raw.githubusercontent.com/Xpra-org/xpra/master/packaging/repos/bionic/xpra.sources
RUN apt update && apt install xpra -y

EXPOSE 8800

# Install ROS
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt install curl gnupg -y
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -

RUN apt update

RUN apt install ros-melodic-desktop-full -y 

RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
# RUN source ~/.bashrc

RUN apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential -y

RUN apt install python-rosdep
RUN rosdep init
RUN rosdep update

RUN mkdir -p ~/catkin_ws/src
# RUN cd ~/catkin_ws && catkin_make
# RUN 

# Install ros example
RUN apt-get install ros-melodic-husky-simulator -y

EXPOSE 8800
ENTRYPOINT ["xpra", "start", "--start=xterm", "--bind-tcp=0.0.0.0:8800", "--no-daemon"]
# ENTRYPOINT ["xpra", "start", ":80", "--bind-tcp=0.0.0.0:8080", \
#  "--mdns=no", "--webcam=no", "--no-daemon","--start=xhost +"]
# CMD ["xpra", "start", "--start=xterm" ,"--bind-tcp=0.0.0.0:8800"]

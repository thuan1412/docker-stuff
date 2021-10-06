FROM centos:centos7

RUN yum -y update; yum clean all
RUN yum -y install openssh-server passwd; yum clean all
RUN yum install -y wget
RUN yum install curl
RUN yum clean all && yum install -y git
# RUN yum clean all && yum install fuse-libs
RUN yum clean all && yum install -y fuse
# RUN curl -o /usr/local/bin/nvim -LO https://github.com/neovim/neovim/releases/download/stable/nvim.appimage

RUN curl -o nvim.appimage -LO https://github.com/neovim/neovim/releases/download/stable/nvim.appimage
RUN chmod u+x /nvim.appimage
RUN /nvim.appimage --appimage-extract
RUN ln -snf /squashfs-root/AppRun /usr/local/bin/nvim
RUN yum install -y nodejs ripgrep

RUN git clone https://github.com/NvChad/NvChad ~/.config/nvim

ADD ./start.sh /start.sh
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN chmod 755 /start.sh
# EXPOSE 22
RUN ./start.sh
ENTRYPOINT ["/usr/sbin/sshd", "-D"]

FROM ubuntu:16.04

# update apt/pip source
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list\
	&& apt-get update \
	&& apt-get install -y apt-transport-https \
	&& cp /etc/apt/sources.list /etc/apt/sources.list.bak \
	&& echo '' > /etc/apt/sources.list \
	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list \
	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list \
	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list \
	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get -y dist-upgrade \
	&& mkdir /root/.pip \
	&& touch /root/.pip/pip.conf \
	&& echo "[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple" > /root/.pip/pip.conf

# install base program
RUN apt-get install -y tmux gcc g++ cmake gdb git nano wget zsh \
	&& chsh -s /bin/zsh \
	&& sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" \
	&& sed -i "s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"ys\"/g" /root/.zshrc \
	&& touch /root/.tmux.conf && echo "set -g mouse on" > /root/.tmux.conf

# install pwntools
RUN apt-get install -y python2.7 python-pip python-dev git libssl-dev libffi-dev build-essential \
	&& pip install --upgrade pip

# fix pip problem and install pwntools
RUN sed -i "s/import main/import __main__/g" /usr/bin/pip \
	&& sed -i "s/main()/__main__._main()/g" /usr/bin/pip \
	&& pip install --upgrade pwntools \
	&& mkdir /root/.pwntools-cache && touch /root/.pwntools-cache/update \
	&& echo "never" > /root/.pwntools-cache/update

# install pwngdb
RUN git clone https://github.com/longld/peda /root/peda \
	&& git clone https://github.com/scwuaptx/Pwngdb /root/Pwngdb \
	&& cp /root/Pwngdb/.gdbinit /root/
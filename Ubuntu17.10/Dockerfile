FROM ubuntu:17.10

# # update apt/pip source
# RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list\
# 	&& apt-get update \
# 	&& apt-get install -y apt-transport-https \
# 	&& apt-get install -y --reinstall ca-certificates \
# 	&& cp /etc/apt/sources.list /etc/apt/sources.list.bak \
# 	&& echo '' > /etc/apt/sources.list \
# 	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic main restricted universe multiverse" > /etc/apt/sources.list \
# 	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-updates main restricted universe multiverse" >> /etc/apt/sources.list \
# 	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-backports main restricted universe multiverse" >> /etc/apt/sources.list \
# 	&& echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ cosmic-security main restricted universe multiverse" >> /etc/apt/sources.list \
# 	&& apt-get update \
# 	&& apt-get -y dist-upgrade \
# 	&& mkdir /root/.pip \
# 	&& touch /root/.pip/pip.conf \
# 	&& echo "[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple" > /root/.pip/pip.conf


RUN apt-get update \
	&& apt-get -y dist-upgrade

# install base program
RUN apt-get install -y tmux gcc g++ cmake gdb git nano wget zsh \
	&& chsh -s /bin/zsh \
	&& sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" \
	&& sed -i "s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"ys\"/g" /root/.zshrc \
	&& touch /root/.tmux.conf && echo "set -g mouse on" > /root/.tmux.conf

# install pwntools
RUN apt-get install -y python3 python3-dev git libssl-dev libffi-dev build-essential \
	&& wget -P ~/ https://bootstrap.pypa.io/pip/3.5/get-pip.py \
	&& python3 ~/get-pip.py 

# fix pip problem and install pwntools
RUN pip3 install --upgrade pwntools \
	&& mkdir /root/.pwntools-cache && touch /root/.pwntools-cache/update \
	&& echo "never" > /root/.pwntools-cache/update

# install pwngdb
RUN git clone https://github.com/longld/peda /root/peda \
	&& git clone https://github.com/scwuaptx/Pwngdb /root/Pwngdb \
	&& cp /root/Pwngdb/.gdbinit /root/
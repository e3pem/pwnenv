from ubuntu:19.04

RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak \
	&& sed -i -r 's/([a-z]{2}\.)?archive.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list \
	&& sed -i -r 's/security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list \
    && apt-get update \
	&& apt-get -y dist-upgrade

# install base program
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y tmux gcc g++ cmake gdb git nano wget zsh \
	&& chsh -s /bin/zsh \
	&& sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" \
	&& sed -i "s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"ys\"/g" /root/.zshrc \
	&& touch /root/.tmux.conf && echo "set -g mouse on" > /root/.tmux.conf

# install pwntools
RUN apt-get install -y python python-dev git libssl-dev libffi-dev build-essential \
	&& wget -P ~/ https://bootstrap.pypa.io/pip/2.7/get-pip.py \
	&& python ~/get-pip.py \
    && pip install --upgrade pip \
	&& pip install --upgrade pwntools \
	&& pip install pathlib2

# update pwntools to newest
RUN git clone --depth 1 git://github.com/Gallopsled/pwntools /root/pwntools \
	&& pip install --upgrade --editable /root/pwntools \
	&& mkdir /root/.pwntools-cache && touch /root/.pwntools-cache/update \
	&& echo "never" > /root/.pwntools-cache/update

# install pwngdb
RUN git clone https://github.com/longld/peda /root/peda \
	&& git clone https://github.com/scwuaptx/Pwngdb /root/Pwngdb \
	&& cp /root/Pwngdb/.gdbinit /root/

# install and 32bit env
RUN dpkg --add-architecture i386 \ 
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1

# # install one_gadget and 32bit env
# RUN dpkg --add-architecture i386 \ 
# 	&& apt-get update \
# 	&& DEBIAN_FRONTEND=noninteractive apt-get install -y ruby gem libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 \
# 	&& gem install one_gadget
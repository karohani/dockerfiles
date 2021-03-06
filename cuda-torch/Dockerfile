FROM carpedm20/cuda
MAINTAINER Taehoon Kim <carpedm20@gmail.com>

# Install dependencies
RUN apt-get update && apt-get install -y \
  curl \
  ipython3 \
  python-zmq

# Run Torch7 installation scripts
RUN curl -sk https://raw.githubusercontent.com/torch/ezinstall/master/install-deps | bash
RUN git clone https://github.com/torch/distro.git ~/torch --recursive
RUN cd ~/torch; ./install.sh

# Install Folly, fbthrift, thpp and fblualib
RUN curl -sk https://raw.githubusercontent.com/facebook/fblualib/master/install_all.sh | bash

# Set ~/torch as working directory
WORKDIR /root/torch

# Export environment variables manually
ENV LUA_PATH='/root/.luarocks/share/lua/5.1/?.lua;/root/.luarocks/share/lua/5.1/?/init.lua;/root/torch/install/share/lua/5.1/?.lua;/root/torch/install/share/lua/5.1/?/init.lua;./?.lua;/root/torch/install/share/luajit-2.1.0-alpha/?.lua;/usr/local/share/lua/5.1/?.lua;/usr/local/share/lua/5.1/?/init.lua' \
  LUA_CPATH='/root/.luarocks/lib/lua/5.1/?.so;/root/torch/install/lib/lua/5.1/?.so;./?.so;/usr/local/lib/lua/5.1/?.so;/usr/local/lib/lua/5.1/loadall.so' \
  PATH=/root/torch/install/bin:$PATH \
  LD_LIBRARY_PATH=/root/torch/install/lib:$LD_LIBRARY_PATH \
  DYLD_LIBRARY_PATH=/root/torch/install/lib:$DYLD_LIBRARY_PATH

# Install basic Torch and lua moduels
RUN luarocks install nngraph && \
  luarocks install optim && \
  luarocks install nn && \
  luarocks install cutorch && \
  luarocks install cunn && \
  luarocks install penlight && \
  luarocks install luautf8

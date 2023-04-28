FROM debian:11
ENV DEBIAN_FRONTEND=noninteractive
RUN sed -i -e's/ main/ main contrib non-free/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y cmake g++ git libmkl-dev occt-misc libocct-data-exchange-dev libocct-draw-dev libxi-dev libxi6 mpi-default-dev python3-dev python3-mpi4py python3-setuptools
WORKDIR /root
RUN mkdir src
WORKDIR /root/src
ENV PYTHONPATH=/opt/netgen/lib/python3/dist-packages/
ENV PATH="/opt/netgen/bin:$PATH"
RUN git clone https://github.com/ngsolve/ngsolve.git
WORKDIR /root/src/ngsolve
RUN git submodule update --init --recursive
RUN mkdir build
WORKDIR /root/src/ngsolve/build
RUN cmake .. -DUSE_MPI=ON -DUSE_MKL=ON -DMKL_INCLUDE_DIR=/usr/include/mkl/
RUN make -j9 install
CMD netgen /root/src/ngsolve/py_tutorials/navierstokes.py

FROM ubuntu:16.04
MAINTAINER Dmitry Mittov <mittov@gmail.com>

RUN apt-get -qq update && \
    apt-get install -y git \
                       g++ \
                       cmake \
                       libboost-program-options-dev \
                       zlib1g-dev \
                       libboost-python-dev \
                       python-pip \
                       python-dev \
                       htop \
                       unzip \
                       wget && \
    pip install --upgrade pip \
                          scipy \
                          numpy && \
    pip install --upgrade sklearn \
                          tqdm \
                          jupyter \
                          matplotlib \
                          seaborn && \
    pip install --upgrade cython && \
    python -m ipykernel.kernelspec

WORKDIR /tmp
RUN git clone https://github.com/JohnLangford/vowpal_wabbit.git
RUN git clone https://github.com/guestwalk/libffm.git
WORKDIR /tmp/vowpal_wabbit
RUN make && make install
WORKDIR /tmp/libffm
RUN make && mv ffm-train /usr/bin/ && mv ffm-predict /usr/bin/
RUN pip install git+https://github.com/coreylynch/pyFM

WORKDIR /tmp
RUN wget http://files.grouplens.org/datasets/movielens/ml-100k.zip
RUN wget http://files.grouplens.org/datasets/movielens/ml-20m.zip

EXPOSE 8888
VOLUME /notebooks
WORKDIR /notebooks

COPY run_jupyter.sh /
CMD ["/run_jupyter.sh"]

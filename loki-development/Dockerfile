FROM ubuntu:24.04 as build

# byacc alone is not enough, we need to install bison/yacc
RUN apt update && apt install -y gcc gfortran meson build-essential git python3 python3-venv python3-pip openjdk-11-jdk bison yacc flex libxml2-dev

ENV JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64/"
ENV OMNI_INSTALL_DIR="/opt/omni/"
# It is enough to make OMNI binaries accesible on the PATH for Loki to correctly
# initialize the OMNI parser.
ENV PATH="/opt/omni/bin:${PATH}"

WORKDIR /home/ubuntu
RUN git clone --recursive --single-branch https://github.com/omni-compiler/xcodeml-tools.git xcodeml-tools

WORKDIR /home/ubuntu/xcodeml-tools
RUN ./configure --prefix="${OMNI_INSTALL_DIR}"
RUN make -j $(nproc)
RUN make install

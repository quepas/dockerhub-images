FROM ubuntu:18.04 as build

# The rest of packages are required by the Python build (at least this what
# one website has told me)
RUN apt update && \
  apt -y upgrade && \
  apt -y install build-essential zlib1g-dev libncurses5-dev \
                 libgdbm-dev libnss3-dev libssl-dev libreadline-dev \
                 libffi-dev libsqlite3-dev wget libbz2-dev pkg-config

WORKDIR /home/ipsl
RUN wget https://www.python.org/ftp/python/3.13.2/Python-3.13.2.tgz && tar -xf Python-3*.tgz && ls && mv Python-3.13.2 python3-src
WORKDIR /home/ipsl/python3-src
RUN ./configure --enable-optimizations --enable-shared
RUN make -j $(nproc)
RUN make install

FROM ubuntu:18.04

# Although this image is rather generic, I install here git for one of my own projects
# git - needed by loki (https://github.com/ecmwf-ifs/loki)
# binutils - needed by PyInstaller (https://pyinstaller.org)
# jq - to parse JSON returnded by pip to figure out the package version
# software-properties-common - adding apt-ppa repository
RUN apt update && \
  apt -y upgrade && \
  apt -y install git binutils jq software-properties-common ca-certificates

COPY --from=build /usr/local/bin/python3.13 /usr/local/bin/python3.13
COPY --from=build /usr/local/lib/python3.13 /usr/local/lib/python3.13
COPY --from=build /usr/local/include/python3.13 /usr/local/include/python3.13
# NOTE: for some reason, the shared libraries are not installed by make in /usr/local/lib/python3.13 
COPY --from=build /home/ipsl/python3-src/libpython3* /usr/local/lib/python3.13/
ENV LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib/python3.13/"

WORKDIR /home

RUN update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.13 10

RUN python3 -m pip install --upgrade pip && python3 -m pip install pyinstaller==6.11.1


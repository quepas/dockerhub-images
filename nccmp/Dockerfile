# Compare content of two NetCDF files using nccmp tool!
# URL: https://gitlab.com/remikz/nccmp
#
# Typical use (go to directory where your files are):
#  cd /path/where/your/files/are/
#  docker run --rm -it -v .:/data quepas/nccmp ./file1.nc ./file2.nc -dfqS
# Flags:
#  -d -> compare data
#  -f -> don't stop at the first difference
#  -q -> be quite
#  -S -> show statistics of differences at the end
FROM alpine:3.20.3 AS build

RUN apk add git cmake gcc g++ make netcdf-dev

WORKDIR /home
RUN git clone https://gitlab.com/remikz/nccmp.git --depth=1 --branch=master
WORKDIR /home/nccmp
RUN cmake . && make -j $(nproc)

FROM alpine:3.20.3

RUN apk add netcdf
COPY --from=build /home/nccmp/src/nccmp/ /home/nccmp

# Turn off HDF5 version mismatch warning
# Not crucial, but something to correct in the future!
# > Warning!  Library version information error.
# > The HDF5 library version information are not consistent in its source code.
# > This is NOT a fatal error but should be corrected.  Setting the environment
# > variable 'HDF5_DISABLE_VERSION_CHECK' to a value of 1 will suppress
# > this warning.
# > Library version information are:
# > H5_VERS_MAJOR=1, H5_VERS_MINOR=14, H5_VERS_RELEASE=4, H5_VERS_SUBRELEASE=2,
# > H5_VERS_INFO=HDF5 library version: 1.14.4
ENV HDF5_DISABLE_VERSION_CHECK=1

# Start on the /data path, allowing for an easy volume bind -v .:/data
# which allows for a natural passing of file paths: ./file1.nc etc.
WORKDIR /data
ENTRYPOINT [ "/home/nccmp"]

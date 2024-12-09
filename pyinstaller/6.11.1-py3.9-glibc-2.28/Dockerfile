FROM python:3.9-rc-slim

# Although this image is rather generic, I install here git for one of my own projects
# git - needed by loki (https://github.com/ecmwf-ifs/loki)
# binutils - needed by PyInstaller (https://pyinstaller.org)
# jq - to parse JSON returnded by pip to figure out the package version
RUN apt update && apt -y install git binutils jq

RUN pip install --upgrade pip && pip install pyinstaller==6.11.1

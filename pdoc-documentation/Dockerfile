# Use Python 3.11 because loki (https://github.com/ecmwf-ifs/loki) doesn't work with 3.12
FROM python:3.11-slim

RUN apt-get update && apt-get install -y git
RUN pip install --upgrade pip
RUN pip install pdoc==14.4.0

CMD bash

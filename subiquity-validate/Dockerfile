# Validate autoinstall script according to JSON schema.
# URL: https://canonical-subiquity.readthedocs-hosted.com/en/latest/howto/autoinstall-validation.html
#
# How to run? (URL: https://stackoverflow.com/a/43099210/1319478)
#   docker run --rm -i quepas/subiquity-validate < /path/to/script
#
FROM ubuntu:24.04

RUN apt update && apt install -y git make sudo

WORKDIR /home
RUN git clone --branch=24.10.1 --depth=1 https://github.com/canonical/subiquity.git
WORKDIR /home/subiquity
RUN make install_deps

# SNAP variable is required, otherwise, the script produces the following error:
#  > Could not find path to SNAP
#  > Failure: The provided autoinstall config failed validation
# URL: https://askubuntu.com/a/1530718/894912
ENV SNAP=/home/subiquity

ENTRYPOINT [ "/home/subiquity/scripts/validate-autoinstall-user-data.py" ]

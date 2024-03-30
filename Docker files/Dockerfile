FROM python:3-slim
MAINTAINER Sebastien Vanhoutte
ARG TARGETPLATFORM
ARG BUILDPLATFORM
RUN echo "I am running on $BUILDPLATFORM, building for $TARGETPLATFORM"
RUN if [ "$TARGETPLATFORM" = "linux/arm/v7" ]; then \
apt-get update &&  apt-get install --no-install-recommends -y gcc git cron libc6-dev; \
else \
apt-get update &&  apt-get install --no-install-recommends -y git cron; \
fi
#RUN apt-get update &&  apt-get install --no-install-recommends -y git cron
# manually installed patched wyze-sdk that supports ScaleX
WORKDIR /
RUN mkdir /wyze-sdk
RUN git clone https://github.com/svanhoutte/wyze-sdk.git 
WORKDIR /wyze-sdk
RUN pip install .
RUN pip install garth
# install fix for sccale code
WORKDIR /
RUN mkdir /wyze_garmin_sync
RUN git clone https://github.com/ronderful/wyze_garmin_sync.git
WORKDIR /wyze_garmin_sync
RUN apt-get remove -y gcc git libc6-dev
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
CMD /usr/bin/entrypoint.sh

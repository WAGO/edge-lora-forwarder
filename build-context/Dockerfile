ARG HAL_VERSION=V0.2.3
ARG PACKET_FORWARDER_VERSION=V0.1.0

FROM debian as base
ARG CERTFILE_URL
ARG HAL_VERSION
ARG PACKET_FORWARDER_VERSION

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y build-essential git curl
RUN curl -ksSL ${CERTFILE_URL} -o /usr/local/share/ca-certificates/wago.crt; exit 0
RUN update-ca-certificates

RUN mkdir /LoRa
WORKDIR /LoRa
RUN git clone https://github.com/Lora-net/picoGW_hal.git -b ${HAL_VERSION}	
RUN git clone https://github.com/Lora-net/picoGW_packet_forwarder.git -b ${PACKET_FORWARDER_VERSION}

RUN sed -i -r "s/0x010a0006/0x010a0004/g" /LoRa/picoGW_hal/libloragw/inc/loragw_mcu.h \
    && make -C picoGW_hal \
    && make -C picoGW_packet_forwarder

RUN mkdir /deploy
WORKDIR /LoRa/picoGW_packet_forwarder
RUN cp lora_pkt_fwd/lora_pkt_fwd /deploy
RUN cp util_ack/util_ack /deploy
RUN cp util_sink/util_sink /deploy
RUN cp util_tx_test/util_tx_test /deploy

FROM debian:stable-slim as final
ARG HAL_VERSION
ARG PACKET_FORWARDER_VERSION
LABEL authors="jens.sparmann@wago.com, dirk.meihoefer@wago.com"
LABEL org.label-schema.vcs-url="https://github.com/WAGO/edge_lora_packet_forwarder"
LABEL picoGW_hal-version=${HAL_VERSION}
LABEL picoGW_packet_forwarder-version=${PACKET_FORWARDER_VERSION}
COPY --from=base /deploy /
ENTRYPOINT ["/lora_pkt_fwd"]



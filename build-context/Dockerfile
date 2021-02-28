FROM debian as base
LABEL authors="<jens.sparmann@wago.com>"
LABEL org.label-schema.vcs-url="https://github.com/WAGO/edge-lora-forwarder"

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y build-essential git

RUN mkdir /LoRa

WORKDIR /LoRa

RUN git clone https://github.com/Lora-net/picoGW_hal.git	

RUN git clone https://github.com/Lora-net/picoGW_packet_forwarder.git

#WORKDIR /LoRa/picoGW_hal/libloragw/inc

#RUN sed s/0x010a0006/0x010a0004/g /LoRa/picoGW_hal/libloragw/inc/loragw_mcu.h	

WORKDIR /LoRa/picoGW_hal
RUN sed -i -r "s/0x010a0006/0x010a0004/g" /LoRa/picoGW_hal/libloragw/inc/loragw_mcu.h \
    && make

WORKDIR /LoRa/picoGW_packet_forwarder
RUN make 


FROM debian:stable-slim as final

LABEL authors="<jens.sparmann@wago.com>"
LABEL org.label-schema.vcs-url="https://github.com/WAGO/edge_lora_packet_forwarder"

COPY --from=base /LoRa /LoRa
WORKDIR /

WORKDIR /LoRa/picoGW_packet_forwarder/lora_pkt_fwd
ENTRYPOINT ["./lora_pkt_fwd"]



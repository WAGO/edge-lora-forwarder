# LoRa-Packet-Forwarder for WAGO Edge Computer 752-940x

## Prerequisites
- Wago Edge Computer 752-940x
- Mikro Tik LoRa Gateway Mini-PCIe-Card (R11e-LoRa8) -> [order@reichelt.de](https://www.reichelt.de/mini-pcie-gateway-karte-lora-wan-mtk-r11e-lora8-p273003.html?CCOUNTRY=445&LANGUAGE=de&trstct=pos_0&nbc=1&&r=1 "reichelt elektronik")
- LoRa Skills

This container can be used to operate a lora card in the Wago Edge Computer. The container serves as a lora packet forwarder.

### For use with Chirpstack see below.

## For use as lora packet forwarder for own projects:

Find out the path to your lora gateway card 
```bash
  dmesg | grep tty
```

Insert the /dev/ttyACMx path to the docker run command under devices

```bash
  docker run -d --restart unless-stopped --device=/dev/ttyACM0 wagoautomation/edge-lora-forwarder
```

Run the container with own conf file

```bash
  docker run -d --restart unless-stopped -v <Path_to_global_conf.json>:/global_conf.json --devices=/dev/ttyACM0 wagoautomation/edge-lora-forwarder
```

## Chirpstack with WAGO Edge Computer 752-940x

Forked from [brocaar/chirpstack-docker](https://github.com/brocaar/chirpstack-docker "brocaar/chirpstack-docker")

Clone the repository and take a look at the configuration files.

```bash
git clone https://github.com/WAGO/edge-lora-forwarder.git
cd chirpstack-docker
```

After you have updated the configuration, you can run the following command to start all Docker containers:

```bash
docker-compose up
```

### Add Network Server

When adding the Network Server in the ChirpStack Application Server web-interface
(see [Network Servers](https://www.chirpstack.io/application-server/use/network-servers/)),
you must enter `chirpstack-network-server:8000` as the Network Server `hostname:IP`.

# LoRa-Packet-Forwarder for Wago Edge Computer 752-940x

## Prerequisites
- Wago Edge Computer 752-940x
- Mikro Tik LoRa Gateway Mini-PCIe-Card (R11e-LoRa8) -> reichelt.de MTK R11E-LORA8
- LoRa Skills

This container can be used to operate a lora card in the Wago Edge Computer. The container serves as a lora packet forwarder.

Find out the path to your lora gateway card 
```bash
  dmesg | grep tty
```

Insert the /dev/ttyACMx path to the docker run command under devices

```bash
  docker run --devices=/dev/ttyACM0 wagoautomation/edge-lora-forwarder
```


Take a look Chripstack...

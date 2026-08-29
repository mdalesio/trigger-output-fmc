# Quartz EEPROM programming

## Preparation

```
sudo apt-get install atftp
virtualenv env
./env/bin/pip install frugy
. env/bin/activate
```

## Readback/Verification

```sh
atftp -g -r FMC1_EEPROM.bin -l /tmp/x 192.168.79.XXX
hexdump -C /tmp/x
```

## Create/Write

Run `createEEPROMs.sh` to produce the desired S/N.  eg. `15`

```sh
./createEEPROMs.sh 15
atftp -p -r FMC1_EEPROM.bin -l EEPROM_015.bin 192.168.79.XXX
```


## Erasing flash

Open CMD/Terminal and run the following:
```
python3 -m esptool erase_region 0xa000 0xFF6000
```

## Flash the Application

Open CMD/Terminal and run the following:
```
python3 -m esptool -b 921600 --after hard_reset write_flash --flash_mode dio --flash_size 16MB --flash_freq 40m 0x1000 ./bin/bootloader.bin 0x8000 ./bin/partition-table.bin 0xd000 ./bin/ota_data_initial.bin 0x10000 ./bin/walabot-home-vblu.bin
```

## Flash the vblu_production provision config
```
python3 ./script/flash_provision_config.py ./script/provision_config_vblu_production.json
```


# walabot-home-falling

## Software Requirements

- Python3 64bit
- `esptool` installed with `python -m pip install esptool` from CMD/Terminal
- [UART Drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

## Erasing flash

Open CMD/Terminal and run the following:
```
python -m esptool erase_region 0xa000 0xFF6000
```

## Flash the Application

Open CMD/Terminal and run the following:
```
python -m esptool -b 921600 --after hard_reset write_flash --flash_mode dio --flash_size 16MB --flash_freq 40m 0x1000 bin\bootloader.bin 0x8000 bin\partition-table.bin 0xd000 bin\ota_data_initial.bin 0x10000 bin\walabot-home-vblu.bin
```

## Button Behavior

Button press is acknowledged after holding it for at least 3 seconds.

| Timing                    | Behavior                          |
| ------------------------- | --------------------------------- |
| Startup without WiFi      | Start smartconfig                 |
| WiFi connection failure   | Restart smartconfig               |
| Paired                    | Unpair and restart smartconfig    |

## Provision

When provisioning, you need to specify the device, you need
to specify the correct server and packages name. See list
bellow for more details.

| project    | package name                   | cloud registry         |
|------------|--------------------------------|------------------------|
| Breathing  | com.walabot.home.esp.breathing | walabot_home_breathing |
| Fall       | com.walabot.home.esp.fall      | walabot_home_fall      |
| HeartRate  | com.walabot.home.esp.heartrate | walabot_home_heartrate |
| Gen2       | com.walabot.home.esp.client    | walabothome-app-cloud  |
| Gen2 (dev) | com.walabot.home.esp.client    | walabot_home_gen2      |

`http_url`:
  - gen2        - https://us-central1-walabot-home.cloudfunctions.net
  - gen2 (dev ) - https://us-central1-walabothome-app-cloud.cloudfunctions.net
  - others      - https://us-central1-vayyarhomedatacollection.cloudfunctions.net
     
`project_id`:
  - gen2     walabot-home
  - dev      walabothome-app-cloud
  - others   vayyarhomedatacollection

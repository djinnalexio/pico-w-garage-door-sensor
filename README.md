# Raspberry Pi Pico W Garage Door Sensor

## Preparing to Flash the Pico W

Before you can flash anything to the Pico W, you have to define a few `secrets` that ESPHome will use when it compiles the program.

Edit the `secrets.yaml` file inside this directory to add the needed information; get a randomly generated api key from the [ESPHome docs API page](https://esphome.io/components/api.html#configuration-variables).

### Flashing Using Docker

In this directory, I run `docker-compose up -d` to start an esphome container that I'll use to flash the Pico.

Then enter the container:

```
$ docker exec -it esphome bash
root@docker-desktop:/config#
```

This drops you into the container inside the `config` directory, which is shared from this repository.

Compile the binary for the garage door sensor:

```
$ esphome compile garage-door.yml
```

Copy the generated binary into the current directory:

```
$ cp .esphome/build/rpi-pico/.pioenvs/rpi-pico/firmware.uf2 ./rpi-pico.uf2
```

Then on your host computer, with the Pico W booted into BOOTSEL mode (hold down the BOOTSEL button while plugging in the USB cable), copy the `rpi-pico.uf2` file over to the Pico W. When the copy is complete, the Pico should reboot and start working as a garage door sensor.

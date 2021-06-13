# CircuitART ESP32S2 TinyUF2 bootloader 

## Build and Flash

### Requirements

- GCC cross compiler and Make

### Step 1 Install prerequisites 
```
sudo apt-get install git wget flex bison gperf python3 python3-pip python3-setuptools cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
```
### Step 2 clone the TinyUF2 repo
``` 
$ git clone --recurse-submodules https://github.com/adafruit/tinyuf2
```
### Step 3 Setup the tool and  the environment variables
``` 
cd ~/tinyuf2/lip/esp-idf
./install.sh
. $HOME/tinyuf2/lip/esp-idf/export.sh
``` 
### Step 3 build Board
```
make BOARD=circuitart_esp32s2core all
```
### Step 4 Flash
```
make BOARD=circuitart_esp32s2core flash
```

## Usage
There are a few ways to enter UF2 mode:

- There is no `ota application` and/or `ota_data` partition is corrupted
- `PIN_BUTTON_UF2` is gnd when 2nd stage bootloader indicator is on e.g **RGB led = Purple**. Note: since most ESP32S2 board implement `GPIO0` as button for 1st stage ROM bootloader, it can be used for dual-purpose button here as well. The difference is the pressing order:
  - Holding `GPIO0` then reset -> ROM bootloader
  - Press reset, see indicator on (purple RGB) then press `GPIO0` -> UF2 bootloader
- `PIN_DOUBLE_RESET_RC` GPIO is attached to an 100K resistor and 1uF Capacitor to serve as 1-bit memory, which hold the pin value long enough for double reset detection. Simply press double reset to enter UF2

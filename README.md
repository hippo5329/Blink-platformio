# Blink platformio

This is a port of Arduino Blink example to platformio.

## Supported boards

portenta_h7_m7, teensy41, teensy40, teensy36, teensy35, teensy31, due, zero, olimex_e407, esp32, nanorp2040connect, pico.

## Install the software

### Prepare

Install essential build tools. Remove brltty package which interferes with CH340 USB serial on some esp32 boards.

    sudo apt remove brltty -y
    sudo apt install python3-venv build-essential cmake git curl -y

### Install Platformio and udev rules

    curl -fsSL -o get-platformio.py https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py
    python3 get-platformio.py
    echo "PATH="$PATH:$HOME/.platformio/penv/bin"" >> ~/.bashrc
    source ~/.bashrc
    curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core/develop/platformio/assets/system/99-platformio-udev.rules | sudo tee /etc/udev/rules.d/99-platformio-udev.rules
    sudo service udev restart
    sudo usermod -a -G dialout $USER
    sudo usermod -a -G plugdev $USER

### Clone example repository

    git clone https://github.com/hippo5329/Blink-platformio.git

## Build and upload

Build and upload to esp32 devkit. The on-board LED should blink every two seconds.

    cd Blink-platformio
    pio run -e esp32 -t upload

## More examples for Arduino

You may find more [examples from Arduino](https://github.com/arduino/arduino-examples). You may try to port them to platformio the way I do.

1. Create a src subdirectory. Move the .ino source into src subdirectory.
2. Copy my platformio.ini. And, optionally, .gitignore.
3. Build, upload and test.

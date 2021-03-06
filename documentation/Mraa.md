# MRAA

> Low Level Skeleton Library for IO Communication on GNU/Linux platforms

> C/C++ library with bindings to JavaScript and Python to interface with the I/O on the Intel® Galileo board, Intel® Edison board, and other platforms. With board detection done at runtime, you can create portable code that works across multiple platforms.

* AIO Sensors requiring an ADC value to be read
* I2C Modules using the i2c bus
* SPI Modules using the SPI bus
* GPIO Modules using GPIOs directly
* PWM Modules using a PWM capable GPIO pin
* UART Modules using a serial connection (RX/TX)

- [MRAA Github](https://github.com/intel-iot-devkit/mraa)

# Manual Installation, Latest Github

## Yocto

```sh
    root@edison:~# git clone https://github.com/intel-iot-devkit/mraa.git
    root@edison:~# mkdir mraa/build && cd $_
    root@edison:~# cmake ..
    root@edison:~# make
    root@edison:~# make install
    root@edison:~# nano /etc/ld.so.conf
    /usr/local/lib/i386-linux-gnu/
    root@edison:~# ldconfig
    root@edison:~# ldconfig -p | grep mraa
    root@edison:~# export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
    root@edison:~# nano ~/.bashrc
    export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
```

## Ubilinux

```sh
    root@ubilinux:~# apt-get update
    root@ubilinux:~# apt-cache search pcre
    root@ubilinux:~# apt-get install libpcre3-dev
    root@ubilinux:~# apt-get install git
    root@ubilinux:~# apt-get install cmake
    root@ubilinux:~# apt-get install python-dev
    root@ubilinux:~# apt-get install swig
    root@ubilinux:~# git clone https://github.com/intel-iot-devkit/mraa.git
    root@ubilinux:~# mkdir mraa/build && cd $_
    root@ubilinux:~# cmake .. -DBUILDSWIGNODE=OFF
    root@ubilinux:~# make
    root@ubilinux:~# make install
    root@ubilinux:~# cd
    root@ubilinux:~# nano /etc/ld.so.conf
    /usr/local/lib/i386-linux-gnu/
    root@ubilinux:~# ldconfig
    root@ubilinux:~# ldconfig -p | grep mraa
    root@ubilinux:~# export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
    root@ubilinux:~# nano ~/.bashrc
    export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
```

Based on [Installing libmraa on Ubilinux for Edison](https://learn.sparkfun.com/tutorials/installing-libmraa-on-ubilinux-for-edison)

# Testing, Opkg

```sh
root@edison:~# opkg list-installed | grep mraa
mraa - 1.0.0-r0
mraa-dev - 1.0.0-r0
mraa-doc - 1.0.0-r0
```

# Upgrade, Opkg

```sh
root@edison:~# opkg install mraa                                                
Package mraa (1.0.0-r0) installed in root is up to date.                        
root@edison:~# 
```


# Hello Mraa

```sh
    root@edison:~# git clone https://github.com/intel-iot-devkit/mraa.git
    root@edison:~# cd mraa/examples
    root@edison:~# gcc -lmraa hellomraa.c -o hellomraa
    root@edison:~# ./hellomraa
     hello mraa
      Version: v0.7.3
      Running on Intel Edison
```

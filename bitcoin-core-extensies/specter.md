sudo apt install libusb-1.0-0-dev libudev-dev python3-pip -y

pip3 install cryptoadvance.specter

python3 -m cryptoadvance.specter server --daemon --host 0.0.0.0

# Kivy Wheel packages for Raspberry Pi

#### By Kristian Lauszus, 2017
_________

A pre-compiled binary of Kivy for the Raspberry Pi. This was compiled on a Raspberry Pi 3 running Raspbian Jessie Lite.

## Instructions

First install the following dependencies:

```bash
sudo apt-get install libgstreamer1.0-dev libmtdev1
```

Clone the repository:

```bash
git clone https://github.com/Lauszus/rpi-kivy-wheel.git
```

Then simply use the commands below to install Kivy 1.10.1:

__Python 2__

```bash
sudo apt-get install python-wheel
sudo pip install --find-links=rpi-kivy-wheel kivy==1.10.1
```

__Python 3__

```bash
sudo apt-get install python3-wheel
sudo pip3 install --find-links=rpi-kivy-wheel kivy==1.10.1
```

## Developers

The packages can be generated using the following steps on a fresh install of Raspbian Lite.

Set the Python version you want to use:

```bash
export PYTHON=python3
export PIP=pip3
```

Install dependencies:

```bash
sudo apt-get install $PYTHON-pip $PYTHON-dev
sudo apt-get install pkg-config libgl1-mesa-dev libgles2-mesa-dev libgstreamer1.0-dev gstreamer1.0-plugins-{bad,base,good,ugly} gstreamer1.0-{omx,alsa}
sudo apt-get install libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev libmtdev-dev
```

Download the latest version of Kivy:

```bash
wget `curl -s https://api.github.com/repos/kivy/kivy/releases/latest | python -mjson.tool | grep 'zipball_url' | cut -d'"' -f4` -O kivy.zip
```

Setup virtual environment:

```bash
sudo $PIP install -U pip virtualenv setuptools
virtualenv --no-site-packages -p $PYTHON rpi-kivy-venv
source rpi-kivy-venv/bin/activate
```

Install Python packages:

```bash
$PIP install pygments docutils cython==0.28.3
```

In this case I install Cython 0.28.3, as needed by Kivy 1.10.1: <https://kivy.org/docs/installation/installation-linux.html#cython>.

Now compile the wheel:

```bash
$PIP wheel --build=rpi-kivy-build --wheel-dir=rpi-kivy-wheel kivy.zip
```

Now make sure that the wheel is working:

```bash
pip install --find-links=rpi-kivy-wheel kivy
python -c 'import kivy'
```

For more information send me an email at <lauszus@gmail.com>.

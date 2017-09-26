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

Then simply use the command below to install Kivy 1.10.0:

__Python 2.7__

```bash
sudo apt-get install python-pygame python-wheel
sudo pip install rpi-kivy-wheel/kivy-1.10.0/Kivy-1.10.0-cp27-cp27mu-linux_armv7l.whl
```

__Python 3.4__

```bash
sudo apt-get install python3-pygame python3-wheel
sudo pip3 install rpi-kivy-wheel/kivy-1.10.0/Kivy-1.10.0-cp34-cp34m-linux_armv7l.whl
```

## Developers

The packages can be generated using the following steps on a fresh install on Raspbian Lite:

Download the latest version of Kivy:

```bash
wget `curl -s https://api.github.com/repos/kivy/kivy/releases/latest | python -mjson.tool | grep 'zipball_url' | cut -d'"' -f4` -O kivy.zip
```

Set the Python version you want to use:

```bash
export PYTHON=python3
export PIP=pip3
```

Install dependencies:

```bash
sudo apt-get install $PYTHON-pygame $PYTHON-setuptools $PYTHON-wheel $PYTHON-pip
sudo apt-get install pkg-config libgl1-mesa-dev libgles2-mesa-dev libgstreamer1.0-dev gstreamer1.0-plugins-{bad,base,good,ugly} gstreamer1.0-{omx,alsa}
```

Install Python packages:

```bash
sudo $PIP install pygments docutils cython==0.25.2
```

In this case I install Cython 0.25.2, as needed by Kivy 1.10.0: <https://kivy.org/docs/installation/installation-linux.html#cython>.

Now compile the wheel:

```bash
$PIP wheel --build=build --wheel-dir=rpi-kivy-wheel kivy.zip
```

Now make sure that the wheel is working:

```bash
virtualenv -p $PYTHON kivy-env
~/kivy-env/bin/pip install -U pip
~/kivy-env/bin/pip install rpi-kivy-wheel/Kivy-*-linux_armv7l.whl
~/kivy-env/bin/python -c 'import kivy'
rm -rf kivy-env/
```

Be sure to remove the build directory afterwards:

```bash
rm -rf build/
```

For more information send me an email at <lauszus@gmail.com>.

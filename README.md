# Hecs

=====================================
###  Mechanical Keyboard Sound As You Type 
 
This project is a fork of the famous project Bucklespring : https://github.com/davelab6/bucklespring

I thought of using mechanical keyboard's sound instead of the old IBM keyboards. The sound used is from Cherry Mx Blue ABS Keyboard.

To temporarily silence hecs, for example to enter secrets, press
ScrollLock twice (but be aware that those ScrollLock events _are_ delivered to
the application); same to unmute. The keycode for muting can be changed with
the `-m` option. Use keycode 0 to disable the mute function.

Installation
------------

### Linux, building from source

To compile on debian-based linux distributions, first make sure the require
libraries and header files are installed, then simply run `make`:

#### Dependencies on Debian
```
$ sudo apt-get install libopenal-dev libalure-dev libxtst-dev
```

#### Dependencies on Arch Linux
```
$ sudo pacman -S openal alure libxtst
```

#### Dependencies on Fedora Linux
```
$ sudo dnf install gcc openal-soft-devel alure-devel libX11-devel libXtst-devel
```

#### Installation
```
$ make
$ sudo make install
```

The default Linux build requires X11 for grabbing events. If you want to use
hecs on the linux console or Wayland display server, you can configure
hecs to read events from the raw input devices in /dev/input. This will
require special permissions for hecs to open the devices, though. Build with

```
$ make libinput=1
```

### Keep it Running

```
Run from
	App launcher : dmenu, rofi 
	Terminal : hecs &
```

<img src="https://github.com/TheRealHex/Hecs/blob/master/snaps/1.gif">

### MacOS

I've heard rumours that hecs also runs on MacOS. I've been told that
the following should do:

```
$ brew install alure pkg-config
$ git clone https://github.com/TheRealHex/hecs-Cherry.git && cd hecs
$ sed -i '' 's/-Wall -Werror/-Wall/' Makefile
$ sudo make install
```

Note that you need superuser privileges to create the event tap on Mac OS X.
Also give your terminal Accessibility rights: system preferences -> security -> privacy -> accessibility

If you want to use hecs while doing normal work, add an & behind the command.
```
$ hecs &
```

### Windows
Sorry not available for now :{-

Usage
-----

````
usage: ./hecs [options]

options:

  -d DEVICE use OpenAL audio device DEVICE
  -f        use a fallback sound for unknown keys
  -g GAIN   set playback gain [0..100]
  -m CODE   use CODE as mute key (default 0x46 for scroll lock)
  -M        start the program muted
  -h        show help
  -l        list available openAL audio devices
  -p PATH   load .ogg files from directory PATH
  -s WIDTH  set stereo width [0..100]
  -v        increase verbosity / debugging
  
````
#### Uninstallation

```
$ sudo make uninstall
```

OpenAL notes
------------
Hecs uses the OpenAL library for mixing samples and providing a
realistic 3D audio playback. This section contains some tips and tricks for
properly tuning OpenAL for Hecs.

* The default OpenAL settings can cause a slight delay in playback. Edit or create
  the OpenAL configuration file `~/.alsoftrc` and add the following options:

 ````
 period_size = 32
 periods = 4
 ````

* If you are using headphones, enabling the head-related-transfer functions in OpenAL
  for a better 3D sound:

 ````
 hrtf = true
 ````

* When starting an OpenAL application, the internal sound card is selected for output,
  and you might not be able to change the device using pavucontrol. The option to select
  an alternate device is present, but choosing the device has no effect. To solve this,
  add the following option to the OpenAL configuration file:

 ````
 allow-moves = true
 ````
 <img src='https://github.com/TheRealHex/Hecs/blob/master/img/cherry-mx-blue.jpg'>

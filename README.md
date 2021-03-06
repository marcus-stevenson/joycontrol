# joycontrol-ms
Emulate Nintendo Switch Controllers over Bluetooth.

Tested on Raspberry Pi 4B

## Features
Emulation of JOYCON_R, JOYCON_L and PRO_CONTROLLER.
- button commands
- stick state
- nfc data
- controller keybinding
- controller macro recording, playback, deleting
- [SparkFun Top pHAT](https://www.sparkfun.com/products/16301?_ga=2.239021640.918075716.1594175635-1216658051.1509937706) integration

## Installation
Set up your Top pHAT by following the guide [here](https://learn.sparkfun.com/tutorials/sparkfun-top-phat-hookup-guide?_ga=2.239584971.918075716.1594175635-1216658051.1509937706)
- Install dependencies

Ubuntu: Install the `dbus-python` `libhidapi-hidraw0` and `keyboard` packages
```bash
sudo apt install python3-dbus libhidapi-hidraw0 keyboard
```

Arch Linux Derivatives: Install the `hidapi` and `bluez-utils-compat`(AUR) packages


- Clone the repository and install the joycontrol package to get missing dependencies (Note: Controller script needs super user rights, so python packages must be installed as root). In the joycontrol folder run:
```bash
sudo pip3 install .
```
- Disable the bluez "input" plugin, see [#8](https://github.com/mart1nro/joycontrol/issues/8)

## Command line interface example
- Run the script
```bash
sudo python3 run_controller_cli.py PRO_CONTROLLER
```
This will create a PRO_CONTROLLER instance waiting for the Switch to connect.

- Open the "Change Grip/Order" menu of the Switch

The Switch only pairs with new controllers in the "Change Grip/Order" menu.

Note: If you already connected an emulated controller once, you can use the reconnect option of the script (-r "\<Switch Bluetooth Mac address>").
This does not require the "Change Grip/Order" menu to be opened. You can find out a paired mac address using the "bluetoothctl" system command.

- After connecting, a command line interface is opened. Note: Press \<enter> if you don't see a prompt.

Call "help" to see a list of available commands.

- If you call "test_buttons", the emulated controller automatically navigates to the "Test Controller Buttons" menu. 


## Issues
- Some bluetooth adapters seem to cause disconnects for reasons unknown, try to use an usb adapter instead 
- Incompatibility with Bluetooth "input" plugin requires a bluetooth restart, see [#8](https://github.com/mart1nro/joycontrol/issues/8)
- It seems like the Switch is slower processing incoming messages while in the "Change Grip/Order" menu.
  This causes flooding of packets and makes pairing somewhat inconsistent.
  Not sure yet what exactly a real controller does to prevent that.
  A workaround is to use the reconnect option after a controller was paired once, so that
  opening of the "Change Grip/Order" menu is not required.
- ...


## Resources

[Nintendo_Switch_Reverse_Engineering](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering)

[console_pairing_session](https://github.com/timmeh87/switchnotes/blob/master/console_pairing_session)

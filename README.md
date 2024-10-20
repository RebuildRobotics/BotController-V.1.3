# BotController-V.1.3
"All-In-One" bluetooth controller designed to control Arduino bots with Android smartphone/tablet.
****************************************
Rebuild {Robotics} - BotController V.1.3
****************************************

"All-In-One" bluetooth controller designed to control Arduino bots with Android smartphone/tablet.

Controller is specially designed to be used together with our designed ESP32-C3 based combat bot scripts found also from our github pages.
It can be used also with self made scripts and without using bot configurations in settings.

*****
Features:
*****
- BluetoothLE 5.0 & 4.0 compatible.
- Specially designed to control 150 g / 450 g combat robots.
- Accurate controls are made with sliders, joysticks and motion, no clumsy driving with buttons.
- 3 different joystick sizes to help in precision driving with touchscreen or with Q8Plus -joystick.
- Adjustable 2 -step linear speed control and channel mixing.
- Haptic feedback from buttons and when driving totally straight forward or backward with joysticks modes (offset area).
- Combat control includes: joystick, weapon control, AI control, invert driving, trim and signal lock screen for safety.
- Customizable, separate profiles for controller and bot.
- Sends data from 4 different "channels" in one signal.
- Battery voltage monitoring and low voltage alarm.
- Optimized for 1920x1080px screen ratio, adaptable for smaller ones.
- Available languages: English, Finnish.

*****
Versions:
*****
When using controller with Rebuild Robotics "CombatBot for Beetle ESP32-C3..." scripts primary version numbers should always match (e.g. Controller: 1.2 - Bot Script: 1.2.1 vice versa).

*****
Ways to connect to device:
*****
- Bluetooth devicelist (filtered/unfiltered)
- NFC
- QR code
- Reconnect to earlier MAC address at startup
- Favorites list

*****
Retrieving bot presets:
*****
Basic bot presets are retrieved automaticly and can be done from controller when using our designed softwares.

*****
Hints:
*****
- Motion controller: screen up = stop, tilt = move.  
- Block incoming phonecalls and messages before competitions, by putting your phone into airplane mode.
- If accidentally turning screen off with system buttons while driving turn phone 180deg around so that the buttons are further away from joystick.
- Combat control can be used to drive combat robots or Arduino bots with servo (Tractors, forklifts..), other controller modes have only driving.
- AI signal can be used for example in semiautomatic flipper, where sensor detects near opponent and flips it automaticly.
- Use autoconnect or save your bots into favorites list before big events to help in devicelisting exhaust.

*****
Notices:
*****
- COMBAT ROBOTICS IS FUN, EDUCATING, BUT DANGEROUS HOBBY. ALWAYS THINK SAFETY FIRST!
- If you are using this app in combat robotics, ROBOT HAS TO INCLUDE PROPER FAILSAFE!
- In combat robotics it is recommended to use our ESP32-C3 based script and ESP32-C3 CombatBot Expansion Board together with ESP32-C3 and HR8833 motor driver. They have been developed together with this controller for that use.
- This controller and our combat robot softwares have been made respecting the regulations of combat robotics and they should be usable all around the world.
- Script builder and component manufacturers are not responciple from possible damages.

*****
SIGNALS:
*****
- Sends data from 4 different "channels" in one signal.
- Signal is formatted as string: ch1:ch2:ch3:ch4 ending to newline character.
- Signal is sent only when one of the channel values has been changed or preset is sent to bot.
- All transmitted values are in percents which are converted into PWM-, PPM ratios and degrees in bots end.
- Transmit interval can be changed from settings.

- Driving: (ch1):
  - Forward: -1 > -100%
  - Backward: 1 > 100%

- Turning: (ch2):
  - Left: -1 > -100%
  - Right: 1 > 100%

- Stop:
  - ch1:0, ch2:0

*****
Combat control only:
*****
- Weapon/Servo (ch3):
  - Bidirectional:
    - Weapon on/Servo pos: -100 > 100%
    - Weapon off/Servo idle: 0

  - Normal:
    - Weapon on/Servo pos: 1 > 100%
    - Weapon off/Servo idle: 0

  Idle/Max/Min angles are handled in bots end.

- AI (ch4):
  - AI on: 100
  - AI off: 0

  Weapon and AI status are defined by bots confirm.

*****
SETTINGS:
*****

*****
CONTROLLER:
*****
These values are used by controller. They are saved into and loaded from controllers memory.

- Profiles:
  - Contains stored controller presets.
  - New profiles can be added by changing values and profile name then saving profile.
  - Selected profile is loaded at controller startup.

- Connection:
  - Reconnect to current MAC address at startup:
    - Automaticly reconnects to previously used address at startup. (Device has to be found from bluetooth device list!).
    - If reconnect fails, bluetooth device list will open and new device can be picked.

  - Transmitting interval:
    - Interval for sending data to bot.
    - Tested: ESP 20ms, SAMD/ATMEGA 200-250ms.

- Driving:
  - Treshold-MaxSpeed:
    Treshold limit after what speed is always counted to max.

  - SpeedMultiplier-Slow:
    Slow speed areas speed multiplier in percents.

  - SpeedMultiplier-Fast:
    Fast speed areas speed multiplier in percents.

  - Treshold-FastSpeed:
    - Limit to adjusts where fast speed area starts. Under value is slow speed area and over value is fast speed area.
    - At default limit is 0 which means that slow speed area is not in use, because fast speed starts from 0% from signal.

- Turning:
  Controls as in driving..

  - Control pads:
    - Turn offset:
      Joysticks turning free center areas width per side in pixels.

    - Size:
      - Size of controller pads. 
      - Use 80px for Q8Plus joystick and other sizes for touchscreen.
      - If having problems to gain full speed with Q8Plus joystick lower maxSpeed-Treshold.

    - Use haptic feedback in joystick:
      - Gives feedback when driving totally straight forward or backward in joysticks modes.
      - Phone vibrates when cursor is in offset area.

*****
Combat control only:
*****
- Hide AI button from weaponmenu:
  Hides AI button from combat controls weaponmenu.

*****
BOT:
*****
These values are used by bot. They are saved into and loaded from bots memory one at time.

- Sent parameter ends in to newline character.

- Name:
  - Bots advertised name.
  - Changing requires bot restart.
  - Set parameter: name (Has to start with character).

- Get presets:
  - Requests customizable bot presets from bot.
  - Paramater to request presets: GET_PRESETS.

- Driving:
  - ChannelMix:
    - Mixes signals from ch1(fwd/bwd) and ch2(left/right) used in driving.

  - Trim:
    - Trim for drivemotors.
    - Get and set parameters: T_L=value, T_R=value, value = 0-100.

  - Invert left side motor rotation:
    - Inverts left side driving motors rotation from bot.
    - Get and set parameter: I_L=value, value = 0 / 1.

  - Invert right side motor rotation:
    - Inverts right side driving motors rotation from bot.
    - Get and set parameter: I_R=value, value = 0 / 1.

*****
Combat control only:
*****
- Servo / Weapon:
  - Use Bidirectional weapon signal:
    - Defines can servo or weapon be used in two directions like in driving.
    - If checked weaponchannels signal is -100 > 100 and if not 0 > 100.
    - Get and set parameter: BI=value, value = 0 / 1.
    - Receiving bot presets toggles also controllers weaponslider to proper directions.

  - Use ESC instead of servo:
    - Defines is signal counted continually or only when it has been changed. Servo needs to be written only once, brushless ESC needs continuous signal.
    - Get and set parameter: ESC=value, value = 0 / 1.

  - Angle-Idle:
    - Angle what bot will set when weaponsignal is 0.
    - Using weaponbutton when weapon is on will set angle to idle.
    - Get and set parameter: S_ID=value, value = 0-180.

  - Angle-Max:
    - Max. angle what bot will set when weaponsignal is 100.
    - Using weaponbutton when weapon is off and birectional is false will set angle to max. If bidirectional is true weaponbutton will only work with idle angle.
    - Get and set parameter: S_MA=value, value = 0-180.

  - Angle-Min:
    - Max. min angle what bot will set when birectional signal is used and weaponsignal is -100.
    - Get and set parameter: S_MI=value, value = 0-180.

*****
Other parameters received from bot:
*****
- Weapon status: WEP=value, value = 0 / 1.
- AI status: AI=value, value = 0 / 1.
- Battery status: BAT=value, value = 0-100.

*****
Further copyrights in programs info section. Third party script writers hasn't got nothing to do with this project except I'm using their libraries.
*****

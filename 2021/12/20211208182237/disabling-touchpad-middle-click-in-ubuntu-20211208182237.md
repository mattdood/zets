---
path: '/2021/12/disabling-touchpad-middle-click-in-ubuntu-20211208182237'
title: 'disabling touchpad middle click in ubuntu'
date: '20211208182237'
category: 'linux'
tags: ['ubuntu', 'xinput']
---

# disabling touchpad middle click in ubuntu
My partner had an incredibly frustrating evening battling with her overly sensitive
touchpad controls on a Lenovo laptop a few nights ago. The primary issue was that
Ubuntu has a few defaults that mixed poorly with FireFox:

Middle mouse clicking will:
1. Paste the clipboard in a text area
1. Close the tab that she's hovering over and attempting to left-click

To remedy this situation I thought it best to just disable the middle click altogether,
this would kill two birds with 1 stone ([especially because FireFox doesn't have a setting
to just disable the middle click on tabs very easily](https://support.mozilla.org/en-US/questions/1254024)).

The [StackOverflow link that saved the day](https://unix.stackexchange.com/questions/438725/disabling-middle-click-on-bottom-of-a-clickpad-touchpad).

## Steps + commands to disable the middle click
1. Open terminal and determine what hardware you currently have

```
xinput list

# example output
matthew@matthew-E490:~/$ xinput list
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=11   [slave  pointer  (2)]
⎜   ↳ TPPS/2 ALPS TrackPoint                    id=12   [slave  pointer  (2)]
⎜   ↳ Logitech G602                             id=15   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=13   [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ Integrated Camera: Integrated C           id=9    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=10   [slave  keyboard (3)]
    ↳ DCMT Technology USB Condenser Microphone  id=14   [slave  keyboard (3)]
    ↳ Logitech G602                             id=16   [slave  keyboard (3)]
    ↳ liliums Lily58                            id=17   [slave  keyboard (3)]

```

1. Take note of the ID of the trackpad (or mouse) you want to disable, mine is `id=11`

1. Disable the button mapping for middle click, while maintaining all other functions
    * Note: The middle click is option `2`, notice that below we're setting this to `0` (unmapped)
        * If we wanted, we could also set this button to the function of an adjacent button (like `1` or `2` for left/right clicking)

```
xinput set-button-map <id> 1 0 3 4 5 6 7 8 9 10 11 12
```


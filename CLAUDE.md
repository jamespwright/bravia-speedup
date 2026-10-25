# bravia-speedup

Make Jim's Sony BRAVIA 4K VH2 (Google TV 12) less laggy by disabling bloat and replacing the
stock launcher, using [cleanyourtv](https://github.com/Gathin23/cleanyourtv) as a pinned submodule.

## The TV

- Product `BRAVIA_VH2_M_PA` (Asia-Pacific "M" firmware), build `STT2.230505.001.S136 682241`, Android 12
- `192.168.0.31`, wired (eth0). ADB on port 5555; the setting is called "ADB debugging" on this firmware
- Jim uses Plex (`com.plexapp.android`) against the Plex server on his Unraid box. He does not use DLNA

## Layout

- `vendor/cleanyourtv/`: upstream, pinned. Don't edit it; change `lists/` instead
- `lists/vh2.txt`: Jim's copy of upstream `examples/sony-bravia-4k-vh2/debloat.txt`. The header says what differs
- `results/`: before/after measurements

## Rules

- Disable only (`pm disable-user`), never uninstall. Apply with `vendor/cleanyourtv/tools/disable.sh`, undo with `restore.sh`
- Measure before and after each change
- Leave launcherx enabled until the replacement launcher is installed and owns HOME. On PA firmware
  launcherx then has to be disabled too (see the notes in the list)
- When finished, turn ADB debugging off on the TV and check port 5555 is closed

# bravia-speedup

Speeds up a Sony BRAVIA 4K VH2 (Google TV) by disabling bloat and swapping the ad-heavy home screen for
a lightweight one. Built on [cleanyourtv](https://github.com/Gathin23/cleanyourtv) (submodule in `vendor/`).

```sh
git clone --recurse-submodules <this repo>
TV_HOST=192.168.0.31 vendor/cleanyourtv/tools/disable.sh lists/vh2.txt
# undo:
TV_HOST=192.168.0.31 vendor/cleanyourtv/tools/restore.sh lists/vh2.txt com.google.android.apps.tv.launcherx
```

Nothing is uninstalled. `disable.sh` saves the TV's state to `~/.cleanyourtv/` first and `restore.sh` replays it.
See `results/` for before/after measurements.

## Launcher

`launcher/config.patch` holds Jim's settings for the cleanyourtv launcher: his dock apps, Sony's Live TV app,
no network button, hold-OK tile menu, and no focus bounce. To rebuild:

```sh
rsync -a vendor/cleanyourtv/launcher/ work/launcher/
patch -d work -p1 < launcher/config.patch
cd work/launcher && ./gradlew assembleRelease   # needs JDK 17 and the Android SDK (sdk.dir in local.properties)
adb -s 192.168.0.31:5555 install -r app/build/outputs/apk/release/app-release.apk
```

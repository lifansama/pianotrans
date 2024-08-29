## Simple GUI for ByteDance's Piano Transcription with Pedals

[![Test](https://github.com/azuwis/pianotrans/actions/workflows/test.yml/badge.svg)](https://github.com/azuwis/pianotrans/actions/workflows/test.yml)

[ByteDance's Piano Transcription][1] is the PyTorch implementation of the
piano transcription system, "High-resolution Piano Transcription with Pedals
by Regressing Onsets and Offsets Times `[1]`".

Using this, we can transcribe piano recordings into MIDI files with pedals.

This is a simple GUI and packaging for Windows and [Nix on Linux/macOS][2].

<p align="center" float="left">
  <img src="screenshots/windows.png" width="49%" />
  <img src="screenshots/macos.png" width="49%" />
  <img src="screenshots/midi.png" width="98.6%" />
</p>

### Requirement

* OS: Windows 7 or later (64-bit), Linux, macOS (Intel/M1)
* Memory: at least 4G

Only Windows 10, Debian Linux 10, and macOS 12.1 M1 are tested.

### How to use on Windows

1. Download [Microsoft Visual C++ Redistributable for Visual Studio 2015, 2017 and 2019][3] `vc_redist_x64.exe` and install
2. Download and unpack [PianoTrans-v1.0.7z][4] (1.5GB download, unpack using [7zip][5])
3. Close other apps to free memory, need at least 2G free memory
4. Run `PianoTrans.exe` in `PianoTrans` directory
5. Choose audio/video files, hold `CTRL` to select multiple files
6. Result MIDI files are in the same directory as the input files

If you want right click menu, run `RightClickMenuRegister.bat`, then you can
select multiple audio/video files, right click and choose `Piano Transcribe`.

PianoTrans automatically uses GPU for inference, if you encounter any problem,
you can try `PianoTrans-CPU.bat` to force using CPU.

### How to use on Linux/macOS using Nix

Note: This howto is for [Nix][2] on Linux/macOS, if you don't use Nix, you can
also follow the upstream [install and usage][6] guide for Python pip instead.

1. Open the terminal
2. Install and setup Nix:
   ``` sh
   sh <(curl -L https://nixos.org/nix/install) --daemon
   mkdir -p ~/.config/nix
   echo 'experimental-features = nix-command flakes' > ~/.config/nix/nix.conf
   ```
   See https://nixos.org/download.html for more details
3. Use Nix to install pianotrans:
   ``` sh
   nix profile install github:azuwis/pianotrans
   ```
4. Run `pianotrans` to open the GUI, choose audio/video files, hold `CTRL`
   (`⌘` for macOS) to select multiple files

For CLI usage, run `pianotrans file1 file2 ...`.

To upgrade pianotrans, run:
``` sh
$ nix profile list
0 github:azuwis/pianotrans#defaultPackage.aarch64-linux github:azuwis/pianotrans/e19d5fd12f4295816fad49f6398e2e53ed2d2b7a#defaultPackage.aarch64-linux /nix/store/zdalndvcralish8d43drzslv0p4pm97v-python3.9-pianotrans-0.2.1
# list nix profiles, `0` is pianotrans
$ nix --option tarball-ttl 1 profile upgrade 0
$ nix profile list
0 github:azuwis/pianotrans#defaultPackage.aarch64-linux github:azuwis/pianotrans/e944720dd0dfcc2b87dcc39c1fdaab086eba4ca6#defaultPackage.aarch64-linux /nix/store/rv5iikrdvc7jrc7mqs8mkc21qh2gklhx-python3.9-pianotrans-1.0
# pianotrans upgraded to v1.0
```

[1]: https://github.com/bytedance/piano_transcription
[2]: https://nixos.org
[3]: https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads
[4]: https://github.com/azuwis/PianoTrans/releases/download/v1.0/PianoTrans-v1.0.7z
[5]: https://www.7-zip.org/download.html
[6]: https://github.com/qiuqiangkong/piano_transcription_inference

### FAQ

Q: Can you improve transcription result?

A: This project is about packaging for https://github.com/bytedance/piano_transcription, as long as it gives you MIDI files, all other issues are out of scope of this project.

You should report to the upstream project here https://github.com/bytedance/piano_transcription/issues

### Changelog

#### [1.0.1] - 2023-02-09

* Add `--cli` option to force disable GUI
* Remove filetypes arg from askopenfilenames to avoid crash
* Update Nix flake, and remove mido/soundfile/torchlibrosa/piano-transcription-inference overlay, all patches accepted in nixpkgs, this means more dependances can be fetched directly from Nix binary cache, less local builds
* Add github test workflow

#### [1.0] - 2022-02-21

* Support Linux/macOS using Nix
* All platforms:
  - Add real GUI alongside CLI
  - GUI allow adding files to transcribe queue
* Windows:
  - Right-click menu supports multiple files (need to re-run `RightClickMenuRegister.bat`)
  - Update pytorch to 1.10.2

#### [0.2.1] - 2021-12-23

* Update pytorch to 1.10.1.
* Update piano-transcription-inference to 0.0.5

#### [0.2] - 2021-09-27

* Update pytorch to 1.9.1.
* Add PianoTrans-CPU.bat to force using CPU for inference.

#### [0.1] - 2021-02-02

* Initial release.

## Cite
`[1]` Qiuqiang Kong, Bochen Li, Xuchen Song, Yuan Wan, and Yuxuan Wang. "High-resolution Piano Transcription with Pedals by Regressing Onsets and Offsets Times." arXiv preprint arXiv:2010.01815 (2020). [[pdf]](https://arxiv.org/pdf/2010.01815.pdf)

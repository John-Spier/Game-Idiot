# Game-Idiot
PSX video/music player and game loader

<img width="640" height="224" alt="image" src="https://github.com/user-attachments/assets/5a968fe8-e721-47ca-9268-6d6189a08442" />

<img width="640" height="224" alt="image" src="https://github.com/user-attachments/assets/43bd9e95-47e9-4296-a569-10da0c111613" />

<img width="640" height="224" alt="image" src="https://github.com/user-attachments/assets/05f37a8e-38dd-4017-82f8-8c593891caff" />

<img width="320" height="224" alt="image" src="https://github.com/user-attachments/assets/3c99573a-e132-41b1-8b7f-25983d721a73" />

## Compiling
Extract EXAMPLE5 from LOWCD.ZIP and create a git repo for the directory, then commit all the files. Afterwards apply the patches. The XMPLAY library will also be needed to compile.

## Supported Formats
Filetypes for VFS/TXT menus are provided in parentheses after the format names. SEQ/VAB, EXE, CDXA, STR, and CDDA are not supported by VFS.

### VT/ParamsV2 (N/A)
Various audio parameters for the SPU.
Format (16 bytes, all 2 byte values are little endian):
Sequence Number (2) - number of the sEP sequence to play, always 0 as SEP is not supported by Game Idiot.
Version (2) - parameters version, only 2 is supported
Loops (2) - number of times to play the track, 0 is infinite
Reverb Volume (1) - SPU reverb volume, 0-127
Reverb Depth (1) - SPU reverb depth, 0-127
Reverb Delay (1) - SPU reverb delay, 0-127
Reverb Type (1) - SPU reverb mode preset, 0-9 (0 is no reverb)
Reverb Feedback (1) - SPU reverb feedback, 0-127
Channels (1) - Audio channel type, 0-4
Volume (1) - Track Volume, 0-127
Master Volume (1) - System Volume, 0-127
Tick Mode (2) - SEQ tick mode, 0-4336

### HITMOD (FFFFFF01)
HIT converted MOD files using MODCONV from Hitmen or [pcsx-redux](https://github.com/grumpycoders/pcsx-redux/tree/main/tools/modconv).

### XM (FFFFFF02)
XM and VAB files converted using XM2PSX from XMPLAY.
Format can be either (ParamsV2) + VAB + XM files appended together, or VAB + XM + (ParamsV2) with [PXMConv](https://github.com/John-Spier/PXMConv).

### VAG (FFFFFF05)
SPU VAG format audio. File must be mono and fit in SPU RAM (512K).

### CDXA Track (00FFFD00 - 00FFFFFF)
Individual track of XA file, last byte is the track number in the file. 00FFFEXX is 2X speed, 00FFFDXX is 1X speed, and 00FFFFXX is automatic speed, which is unstable for individual tracks not selected from an XA file menu.

### CDDA Track (FFFFFF07)
Individual CDDA track. Filename in hex is track number.

### TIM Image (FFFFFF08)
TIM texture image, opens in viewer.

### PSX-EXE (FFFFFF13, FFFFFF14, all others)
PSX EXE file, loaded using BIOS functions. Not compatible with more than 30 files in directory. FFFFFF13 loads stack location and stack size from file, FFFFFF14 loads only stack location, and all other types are used as the stack location.

### STR (FFFFFF0A, FFFFFF0B, FFFFFF0C)
Video converted to STR with Movie Converter or [psxavenc](https://github.com/WonderfulToolchain/psxavenc). FFFFFF0A is automatic speed, FFFFFF0B is 1X speed, and FFFFFF0C is 2X speed.

### VAB (FFFFFF0F)
VAB files for SEQs. Cannot be played directly. Can be created with various tools or extracted from PSF files or games.

### SEQ (01020000 - 0102FFFF)
SEQ music sequences, will need VAB (file index filetype - 01020000) to play, optionally appended to a ParamsV2 file. [PXMConv](https://github.com/John-Spier/PXMConv) can also be used, with the ParamsV2 file coming after the SEQ file. Can be converted from MIDI files or extracted from PSF files using [PSFParamFinder](https://github.com/John-Spier/PsfParamFinder).

### SYSTEM.CNF (FFFFFF16)
Game disc boot file, sets various systems settings and loads the EXE listed in the file.

### TXT (FFFFFFFF)
Automatically selects a TXT menu file format.

### VFS (FFFFFFFE)
Sector aligned file archive. Can be created with [PSFParamFinder](https://github.com/John-Spier/PsfParamFinder) or [VFSTool](https://github.com/John-Spier/VFSTool).

### CDDA Menu (FFFFFFFA)
A menu of all audio tracks on the CD.

### CDXA Menu (FFFFFFF9, FFFFFFF8, FFFFFFF7)
A menu of all tracks in a CDXA file, which can be created with Movie Converter or [psxavenc](https://github.com/WonderfulToolchain/psxavenc). FFFFFFF9 is automatic speed, FFFFFFF8 is 2X speed, and FFFFFFF7 is 1X speed.

### Loser's PROGRAMS.TXT (FFFFFFF6)
A menu of executable files on disc, compatible with Loser's Boot Menu. Can be automatically generated with [ProgramsTxtMaker](https://github.com/John-Spier/ProgramsTxtMaker).

### PSFMenu TITLES.TXT (FFFFFFF5)
A menu of various files on disc, compatible with [PSFMenu](https://github.com/John-Spier/PSFMenu). Can be automatically generated with [ProgramsTxtMaker](https://github.com/John-Spier/ProgramsTxtMaker).

### P.I.M.P. NAMES.TXT (FFFFFFF3)
A menu of STR files on disc, compatible with P.I.M.P.

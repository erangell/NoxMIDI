# Bank Street Music Writer to MIDI Conversion for Nox Archaist

1. When starting a new song project, copy the disk images BSMWMID1, BSMWMID2, and BSMWLOG
   to new filenames.  Example disk images with music data are found in BSMWMID1A, 
   BSMWMID2A, BSMWMID2B, BSMWLOG1, and BSMWLOG2.  While working on your project, make
   sure there is enough disk space on your BSMWLOG disk by deleting any TXT files that
   are no longer needed.

2. Use your copies of BSMWPGM1.dsk and BSMWNOX1.dsk (BSMW data disk) to create songs.  
For best results, add rests to any voices that do not end at a barline.
(There may be bugs in the logic that brings all voices together at each bar).

3. Boot Applewin with your BSMWMID1.dsk in drive 1 and BSMWNOX1.dsk in drive 2.

4. RUN EXTRACT.  
	Swap the disks in drive 1 and 2.
	Enter 0 as the directory sector.
	Select the song to be extracted.
	The program gives you a BSAVE command to copy.  Add ",D2" at the end.

5. Use Copy 2+ to copy your song files to BSMWMID2.dsk in the WORK subdirectory.

6. Boot Applewin with BSMWMID2.dsk in drive 1 and BSMWLOG.dsk in drive 2.

7. RUN BSMW.READER
	Enter filename of the file you extracted from BSMW.
	Set the emulator speed to the fastest setting
	The program displays a Repeat Map at the end.  This is also on the BSMWLOG disk.
	Make notes about the segments you want to repeat based on the song structure.
	The WORK directory has 6 files with MIDI data from each voice of the song.
	PR#3 and CATALOG to see the length of each of those voice files.

10. RUN REPEATS
	Enter song name (the same as the BSMW file you extracted)
	Enter voice number (0-6) to be processed.  Program will be run for each voice
	The repeat map is read from the BSMWLOG.dsk disk and displayed.
	First column = segment number
	2nd column = repeat type: 
		0 = beginning of song
		1 = left repeat
		2 = right repeat
		3 = 1st ending
		4 = 2nd ending
		99 = end of song
	Enter the segments of the song to be added in order.
	The first segment should have FROM = 0
	The last segment should have TO = the segment number with repeat type 99.
	The remaining 6 numbers in each row are the length of the segment for each voice.
	After entering the FROM, TO for the last segment, enter 0,0
	A BSAVE command is displayed.  The song name is prefixed with "E"
	Save each voice file in the root directory of BSMWMID1.dsk
	The number suffixes must be consecutive.  Ex: if you skip voice 1, save voice 2 as .1

Note: The BSAVE command is now automatically executed, allowing the use of executable text files.

The repeats for COMBAT1 are:
0,3  0,6  4,5  6,7  0,3  0,6  4,5  6,8 

The repeats for TOWN1 are:
0,3  0,2  3,6  4,5  6,9  7,8  9,10

You may want to copy or rename track files at this point.
For example, if you are using voices 1 and 3, you may want to rename track 3 as track 2.
See text file: RPTCOMBAT as an example


8. RUN FIXZEROS (in the root of BSMWMID1.dsk)
	BLOADs each voice file that has music data at address 8192 ($2000)\
	BSAVEs the file with ,A$2000 and ,L = length from the CATALOG

9. RUN FIXNOTES
	Same process as FIXZEROS.
	Inserts a delay delta time of 15 between repeated notes within each voice.


11. LOAD MAKE.MIDI.FILE
	LIST the program and edit variables as desired for your midi file.
	FI$ = filename of the .MID file
	NT = number of tracks.  FM=1 = midi format 1, which adds 1 extra track.
	T$= title
	C$= copyright
	MM = metronome setting for tempo
	Time Signature: NN, DD, CC, BB based on the MIDI File Format spec.
	SF = Key signature: Positive = sharps, negative=flats
	MI = Minor (1=yes)
	I$(n) = Instrument name for track n
	SAVE the program with a name that includes the song, in case you need it later.
	RUN the program.  It generates a .MID file for the song.

12. Use Ciderpress or another disk image utility to extract the .MID file to Windows.

You can then test playing the .MID file.  Repeat any of the steps above until it sounds good.
Use the TXT files on the BSMWLOG disk for debugging.

BSMW to MIDI conversion is published in the public domain.
License: https://creativecommons.org/licenses/by/3.0/us/

The Mockingboard driver for Nox Archaist is a custom version of 
"MIDI to Mockingboard Conversion", Copyright 2017, Naspite Labs.

If you want to convert MIDI files to files which can be played on a Mockingboard, please
contact Naspite Labs at: treehouse2000us@yahoo.com

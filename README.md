# Music Converter
Converts entire library to specified format, ignoring files that were previously converted. It currently only works in Unix-like systems due to glob, but it shouldn't be hard to adapt for Windows.

## Usage
```python
archive_path = '/path/to/main/library'
portable_path = '/path/to/converted/library'

converter = MusicConverter(archive_path, portable_path, 'MP3Audio', 'standard')
converter.run()
```
The first three arguments you see there are archive_path, portable_path, and format. The fourth, optional argument is quality. The default quality for mp3 is "standard", so you could actually achieve the same thing by replacing the instantiation line with:
```python
converter = MusicConverter(archive_path, portable_path, 'MP3Audio')
```

### archive_path and portable_path
Paths for your music library. archive_path is what you are converting, and portable_path is where you want the converted files.

### format
Pick one of the audiotools.AVAILABLE_TYPES from http://audiotools.sourceforge.net/programming/audiotools.html and input it as a string to the MusicConverter object.

AACAudio, OggFlacAudio, and ShortenAudio appear to be unsupported in Audiotools despite being listed in the documentation. If you find these work for you, you should uncomment those lines in the source. Here are the formats currently supported without requiring any modification:
- AiffAudio
- ALACAudio
- AuAudio
- FlacAudio
- M4AAudio
- MP3Audio
- MP2Audio
- OpusAudio
- SpeexAudio
- VorbisAudio
- WaveAudio
- WavPackAudio

### quality
Every format has its own set of compression levels which are stored in audiotools.AudioFile.COMPRESSION_MODES. You can use the same strings that are used in Audiotools. Here we can see what is available for MP3:
```python
    DEFAULT_COMPRESSION = "2"
    # 0 is better quality/lower compression
    # 9 is worse quality/higher compression
    COMPRESSION_MODES = ("0", "1", "2", "3", "4", "5", "6",
                         "medium", "standard", "extreme", "insane")
    COMPRESSION_DESCRIPTIONS = {"0": COMP_LAME_0,
                                "6": COMP_LAME_6,
                                "medium": COMP_LAME_MEDIUM,
                                "standard": COMP_LAME_STANDARD,
                                "extreme": COMP_LAME_EXTREME,
                                "insane": COMP_LAME_INSANE}
```
Standard is another name for V2, as you can see here: http://wiki.hydrogenaud.io/index.php?title=LAME#Recommended_settings_details

### Another example
Here is how I use it to squeeze as much as possible on a microSD card. OpusAudio defaults to 96 kbps (which actually sounds decent).
```python
archive_path = '/path/to/main/library'
portable_path = '/path/to/converted/library'

converter = MusicConverter(archive_path, portable_path, 'OpusAudio')
converter.run()
```

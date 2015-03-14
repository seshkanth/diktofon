## Android Market ranking of voice recorder apps in 2011-05-12 ##

```
Top free in "Music & Audio":

79. AndRecorder - Free
109. Hi-Q MP3 Recorder (Lite)

Top paid in "Music and Audio":

16. TapeMachine Recorder
20. Hi-Q MP3 Recorder (Full)
44. RecForge Pro - Audio Record
75. AndRecorder - Premium
78. Audio Recorder Machine


Top free in "Productivity":

21. Voice Recorder
28. Tape-a-Talk Voice Recorder
83. PCM Recorder

Top paid in productivity: /nothing in top ~150/
```


## Activity stack test ##

  1. Launch Diktofon
  1. R&L & start playback
  1. BACK (R&L notification is put up)
  1. Recorder & start recording
  1. HOME (Recorder notification is put up)
  1. R&L: using notification
  1. HOME (R&L is now at the top of the stack)
  1. Recorder: using notification

We should gain access to the existing Recorder, ACTIVITY\_CLEAR\_TOP is a way to achieve that.

## Performance on Samsung Galaxy S II ##

Fresh start / reloading

  * 147 recordings (~1.1GB)
  * 139 tags
  * 113 tokens
  * 108 transcriptions

takes ~8 seconds.

Sorting is instantaneous.

Opening a 7254-word transcription (55 min long radio show) is almost instantaneous.

Searching this transcription is almost instantaneous provided that there is a reasonable number matches (highlighting takes time). Searching for _e_ (4821 matches) and highlighting it takes ~8 seconds.
# Release Notes #

## v0.9.80 (2013-03-21) (released on Google Play: 2013-03-21) ##

  * refreshed menu icons (taken from the SDK)
  * increase font for 7" devices
  * incoming SEND now accepts `video/*`
  * minor UI fixes

## v0.9.79 (2013-03-18) ##

  * fix [Issue 19](https://code.google.com/p/diktofon/issues/detail?id=19)
  * fix [Issue 20](https://code.google.com/p/diktofon/issues/detail?id=20)
  * (experimental) draw transcription turn in grey color if the duration of the turn is very long compared to the number of words in it

## v0.9.78 (2012-08-24) (released on Google Play: 2012-08-24) ##

  * set target SDK = 10
  * don't require microphone hardware

## v0.9.76 (2012-05-12) (released on Google Play: 2012-05-12) ##

  * improved VU meter
  * minor UI changes
  * longer Estonian About-page

## v0.9.74 (2012-05-09) ##

  * improved the recorder (should work on more devices now)
  * improved the sharing of audio files (should work with more apps now)

## v0.9.72 (2011-11-28) (released on Android Market: 2011-12-02) ##

  * improved support for externally recorded audio files
    * e.g. the type of flac-files is now shown correctly, and they can also be transcribed (and probably also played on Android 3.1+)

## v0.9.71 (2011-11-27) ##

  * support for incoming SEND-intent, i.e. other apps can push audio files into Diktofon's collection using their share/send menu. This works with some recorders, file managers, and podcast apps. See also:
    * [Issue 11](https://code.google.com/p/diktofon/issues/detail?id=11)
    * [Intents](Intents.md)

## v0.9.70 (2011-07-06) ##

  * new feature: the search bar now contains the microphone button allowing for voice search (see also: [issue 9](https://code.google.com/p/diktofon/issues/detail?id=9))
  * changed the GUI of the recorder activity
    * record button now contains text/instructions (instead of the microphone image)
    * byte size indicator is smaller and shows one place after the comma
    * there is no title bar
  * changed most of the activities to use the Light-theme (more work is needed to make the styles more consistent and configurable)
  * fixed: [issue 5](https://code.google.com/p/diktofon/issues/detail?id=5)

## v0.9.67 (2011-06-08) (released on Android Market) ##

  * fixed: [issue 4](https://code.google.com/p/diktofon/issues/detail?id=4)
  * recorder button now rectangular (on any screen resolution)

## v0.9.66 (2011-05-24) (released on Android Market) ##

  * fixed: crash when launching via QSB

## v0.9.65 (2011-05-20) (released on Android Market) ##

  * new launcher icon
  * some cleanup and a few bugfixes

## v0.9.60 (2011-05-18) ##

  * added: statusbar notification icons for Recorder and Player services
  * fixed: a few bugs and regressions
  * disabled: Recorder-activity as an alternative entry into Diktofon

## v0.9.59 (2011-05-16) ##

  * improved: Share-menu: now there are 3 options what to share: only transcription, only audio, everything ("only audio" crashes GMail)
  * changed: seconds are not shown in the title of the recording
  * added (experimental): Recorder-activity is now an alternative entry point into Diktofon (from the HOME screen)
  * added: confirmation dialog when leaving the Recorder-activity
  * added (untested): Recorder-activity: now responds to: android.intent.action.PICK
  * added: Recorder-activity: now responds to: RECORD\_SOUND, the standard recorder intent. I.e. Recorder-activity can be now called from other applications. In this case it stores the recordings into the recorder-directory.
  * changed: the activity chooser is shown for the recorder intent only if the user has not already chosen the default. (To clear the default: Settings -> Manage Applications -> /default recorder/ -> Clear settings)
  * lots of internal cleanup

## v0.9.57 (2011-04-05) ##

  * improved: handling of the situation when the playback or recording is in progress, and HOME is pressed. When HOME is pressed then the activity gets hidden but is not destroyed. This situation was not handled properly before, e.g. the GUI got frozen after returning from HOME, Audio Recorder got released, etc. Now the handling of this situation should be better, offering some flexibility e.g. one can pause the recording and search for something on the phone, one can record the current playback, one can take/make a phone call while recording, etc.
  * added: status bar notification is put up if recording or playback is in progress but the corresponding activity is stopped (e.g. HOME-key is pressed). This offers a convenient entry point back into the activity.
  * fixed: amr-mime is again "audio/AMR" ("audio/amr" does not seem to work)
  * fixed: recording list is now initially sorted by timestamp
  * fixed: R&L: query highlighting is not done if there is no transcription
  * improved: nicer recording list item separator

## v0.9.55 (2011-04-02) (released on Android Market) ##

  * changed: the experimental Speaker-support is now hidden, i.e. removed all the Speaker-menus but clicking on the speaker label in the Read&Listen activity still works
  * changed: audio file picking is now called importing (et: importimine)
  * added: recording list items now show a different background when pressed
  * added: app description (which is shown in the Android app manager)
  * fixed: file picker crashed because file:/// URIs were not handled correctly
  * fixed: scrolling to the remembered position in the Read&Listen now works
  * fixed: chronometer showed wrong time when recording started

## v0.9.53 (2011-03-31) ##

  * some fixes to the Speaker support
  * some GUI improvements, e.g. a message is shown if ListView is empty

## v0.9.52 (2011-03-24) ##

  * preliminary support for Speakers
    * new Speaker activity: add/remove/edit speakers, select a speaker
    * changed Read&Listen activity: clicking on a nameless speaker's label creates a mapping to a speaker (whose name will be used as the new label)
  * initial loading time now shorter (by about 20%)
  * added: audio file picking (will open an external file picker and copy the result into the recordings directory)
  * now movable to SD card
  * some GUI improvements
  * major code cleanup

## v0.9.50 (2011-03-11) (released on Android Market) ##

Minor changes:
  * TagSelector: now has fast scroll handle and slightly different layout
  * all activities are now fixed to portrait mode

## v0.9.42 (2011-03-10) ##

Minor changes:
  * TagSelector activity improved
    * nicer layout
    * "Add tags" disabled when TagSelector is used to formulate a query
    * added fast scroll handle
    * selected tags are shown first, then the rest of the tags in alphabetical order
  * now supporting "broken bar" in regexp queries, as alternative for "vertical bar"
  * updated Estonian localization
  * now reporting remaining wait time when waiting for the transcription (the time is updated whenever the recording list is refreshed, e.g. sorted, searched)

## v0.9.40 (2011-03-07) ##

  * added: new tag selector activity which is used for changing the tags of a recording, as well as selecting tags by which to rank the recording list
  * improved: now providing a useful User-Agent string when interacting with the transcription-server: EstSpeechApi/0.0.1 (Diktofon/0.9.40)

## v0.9.30 (2011-03-04) ##

  * fixed: tags are now sorted when displayed in the recording list
  * added: integration into Quick Search Box
  * changed: file sizes are now reported in b, kB, and MB (previously always kB). Note that the recorder reports the current size still in kB.
  * added: new method of changing tags (with a dialog + checkboxes) and adding (new) tags (with a textfield)
  * removed: context menus: "add tag" and "remove tag" (which were made obsolete by the new tag editing facilities)
  * search now sorts untranscribed recordings with no :notrans-tag to the very end of the list
  * generalized "tag value" to multiple tags (but there is no GUI yet to profit from this)

## v0.9.20 (2011-02-25) (first release on Android Market) ##


## v0.9.19 (2011-02-23) ##

  * many changes to GUI (font sizes, colors, new launcher icon)
  * Estonian localization is now complete
  * now memorizing and suggesting search queries
  * added: more text to the About-activity
  * removed: settings: locale forcing
  * disabled: settings: 8-bit recording
  * many bugfixes


## v0.9.10 (2011-02-18) ##

Many changes and fixes, highlights:

  * now showing (and sorting by) the number of speakers
  * highlighting the speakers in the transcription
  * clicking on a paragraph will perform seek+play
  * selecting a tag will order the recordings by "tag value"
  * most activities are locked to portrait-orientation
  * minimum SDK lowered to 4 (i.e. Android v1.6)
  * progress monitor dialog shown during loading of the recordings/transcriptions (the initial loading can take some time, e.g. loading of 400 MB of data takes about 20 sec on HTC Wildfire)

## v0.8.17 (2011-02-09) ##

  * added: sorting by search query match count (triggered right after search)
  * added: sorting by word count (can be used to group together untranscribed notes)
  * added: disabling certain context menu items (transcribe, remove tag) if they don't make sense
  * removed: sorting by transcription status (use sort by word count instead)
  * fixed: recording ID was not unique, now the ID is the full file name (token, transcription and tag files need to be renamed)
  * refactoring: strings and colors are now externalized
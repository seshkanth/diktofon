# Introduction #

The following describes the Activities and GUI in the _Diktofon_ app. Not all of it is implemented yet.

See the [screenshots](http://www.dropbox.com/gallery/1397729/1/Diktofon?h=f5af73).

# Activities #
## Recorder ##

In principle, this is an optional activity, because it can be replaced with an external recorder which has the same interface. Unfortunately, very few existing recorders respond to the recording intent.

Important features:

  * High quality (i.e. 16 bit and 16kHz) recording.
  * Small file size (i.e. less than 20MB even with longer recordings)

Solution: use Android's class AudioRecord which allows for high quality recording even with versions earlier than v2.2. Compress the result to ogg (**NOT IMPLEMENTED**).

GUI:

  * Big button which allows to start/pause/resume recording
  * Timer
  * Current file size indicator
  * VU meter
  * **NOT IMPLEMENTED** Bookmark button (to store one or more positions in time in the recording which one wants to quickly access later)

Should be solid GUI, i.e. shouldn't rotate.

Input/Output:

  * IN: file path onto which to record
  * OUT: file path onto which the recording was made; duration; mime type; bookmarks


## Settings ##

(Booleans/checkboxes have a question mark in the list below.)

  * Use external recorder?
  * Use external recording viewer?
  * Use audio file picker instead of recorder?
  * Audio settings: sampling rate, resolution, compression (ogg/mp3)
  * Transcription settings: server, language, email for identification, polling frequency, ...
  * GUI settings: number of lines of transcription to show in the recording list, day/night mode (i.e. black text on white background vs white text on black background), ...
  * Other: autotranscribe?, autoshare?, ...


Persistency:

  * All the settings

Most of it is currently **NOT IMPLEMENTED**.

## List of recordings ##

Main activity.
Scrollable list of recordings. Each list item comes with a few bits of info about the recording + a context menu.

Info bits:

  * position number
  * timestamp
  * audio info: content type, length in minutes, length in bytes
  * transcription info: length in words, snippet of the beginning, number of speakers
  * tags


Context menu:

  * View (opens _Transcription viewer_)
  * (Re)transcribe (background task; starts the transcription effort, updating the GUI when results are coming in)
  * **NOT IMPLEMENTED** Share via email and social media
  * Add/remove/edit tag or star
  * Properties: more expanded info bits, plus technical bits: ID, path on the file system, transcription status, ...
  * Delete (deletes the recording with Yes/No-confirmation)

Global menu:

  * Record, i.e. launch a voice recorder, or an audio file picker; add the result to the list (optionally immediately transcribed)
  * Search, i.e. rank/filter/highlight the list of recordings using the search query
  * Sort, i.e. sort the list by timestamp, size (in words, seconds, bytes), tags, transcription status, viewing date, number of speakers
  * Settings
  * Transcribe all the untranscribed recordings (with Yes/No confirmation)
  * Reload all recordings from the backend (file system, DB, webstorage). This is done during the launch, it shouldn't be normally needed later.
  * **NOT IMPLEMENTED** Help
  * Tags (opens the tag view: tag editing, filter/highlight recordings by tag, ...)
  * About

Touch:

  * Scrolling
  * Short click: opens _Transcription viewer_
  * Long click: opens the recording's context menu

Search (different options):

  * case sensitive vs insensitive
  * regexp search (e.g. find all recordings that contain a word that is longer than 10 letters)
  * boolean search (e.g. "Ansip AND Savisaar AND NOT Laar")
  * morphology-aware search (i.e. lemmatize the transcription for search purposes, and require the query to contain only lemmas)
  * result should be numerical (e.g. the number of matches) to allow for ranking

## Transcription viewer ##

Displays the transcribed recording (Trans-file which identifies speakers and provides timing information) highlighting paragraphs, speakers, bookmarks. And the current position in the playback. Also the words that match the latest search are highlighted. I.e. something similar to
[Transcribed Speech Archive Browser (TSAB)](http://bark.phon.ioc.ee/tsab/p/play?trans=18).

Global menu:

  * Search (e.g. case-insensitive regexp highlighting)
  * **NOT IMPLEMENTED** Controls for moving around in the text (prev/next search result, prev/next bookmark)
  * Controls for playback (play/pause, fast back/fwd)
  * Share via email and social media

Touch:

  * Scrolling
  * Seek bar
  * Touch a paragraph to play its corresponding audio.
  * **NOT IMPLEMENTED** Pinch to zoom

Persistency:

  * Playback position
  * Zoom level

The current version displays the transcription with an option to seek+play the audio when a paragraph is clicked on. Also the speakers are highlighted in the text.

# Future work #

One major extension _not_ described above is a possibility for a real time transcription with voice commands for correcting the transcription.

Another extension has to do with **Speakers**: filtering recordings by speakers, speaker statistics, extract sentences with the same speaker and paste together a new recording (i.e. new audio + new transcription), etc.

Another extension: recognizing named entities (dates, persons, institutions) that are mentioned in the text. Also better detection of non-speech (music, etc.).
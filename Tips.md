

# Using an external recorder #

Diktofon offers the option of using another installed Android app to obtain the audio recording. This is useful if you have a favorite recorder app which you want to keep using also from within Diktofon, or if you want to profit from a recorder feature which is not available in the Diktofon's own recorder (such as audio compression into mp3 or ogg). In order for the external recorder to be callable from within Diktofon, it must respond to the Android standard intent

```
MediaStore.Audio.Media.RECORD_SOUND_ACTION
```

The following is a list of recorders which we have found to respond to this intent and which are thus usable from Diktofon:

  * [RecForge Free](https://market.android.com/details?id=dje073.android.audiorecorderlite)

(This list is unfortunately very short. If you find a recorder that works with Diktofon, but that is not in this list, please add comment to this page.)

# What is stored on the SD card #

Most of the data that Diktofon manipulates it stores on the SD card and so the data becomes accessible via a file explorer, i.e. it is easy to connect the phone to the computer to backup all the recordings/transcriptions, or to copy new recordings to the phone.
(Only the state of the settings and recording playback positions are stored into an internal preferences database that is not directly accessible to the user.)

The data is stored in the direcotry `Android/data/kaljurand_at_gmail_dot_com.diktofon` which has the following layout:

```
./kaljurand_at_gmail_dot_com.diktofon
./kaljurand_at_gmail_dot_com.diktofon/files
./kaljurand_at_gmail_dot_com.diktofon/files/recordings
./kaljurand_at_gmail_dot_com.diktofon/files/tokens
./kaljurand_at_gmail_dot_com.diktofon/files/trans
./kaljurand_at_gmail_dot_com.diktofon/files/tags
```

Subdirectories:

  * recordings: audio files (in wav, ogg, and mp3)
  * tokens: transcription server tokens (short strings that identify the recording on the transcription server)
  * trans: transcriptions (UTF8 XML-files in Trans-format)
  * tags: tags as whitespace-separated strings

If you have a set of existing voice recordings which you want to transcribe, then copy them into the recordings-directory, then open the Diktofon app, then execute "Reload all", and finally execute "Transcribe all".

# Repairing broken audio files #

It can happen that Diktofon's own recorder crashes while recording. In this case the header of the audio file is not written (the header contains information about the length, sample rate and bit resolution of the audio data) and Diktofon fails to open the file afterwards.

To repair the audio file:

  * find it on the SD card (see the previous section)
  * import it with Audacity (http://audacity.sourceforge.net/) as raw data (Import -> Raw Data)
  * ... using the following settings (assuming that you have not manually overridden Diktofon's sample rate):
    * Encoding: Signed 16 bit PCM
    * Byte order: Little-endian
    * Channels: 1 Channel (Mono)
    * Sample rate: 16000 Hz (or the value that you have configured Diktofon to use)
  * save/export the file.

In most cases you will be able to recover the audio that was recorded before the crash. In general, it is recommended to use an external recording app to make longer recordings, and use Diktofon only to manage and transcribe the recorded files.

# Tags #

## The :notrans tag ##

Assigning the **:notrans** tag to a recording will block it from being transcribed, useful if you want to apply "Transcribe all" but want to exclude a few recordings.

## Ranking by multiple tags ##

The tag menu allows you to select multiple tags (query _q_) in order to rank the list of recordings (_r_). The ranking is given by a **tag value**  _TV_ which is defined like this:

```
TV(r, q) = 100 * | t(r) AND q | - | t(r) |
```

where t(r) is the set of tags of the recording, q is the set of tags in the query, AND is the set intersection, |.| is the set power.

In other words, recordings which only have the selected tags are ranked to the top, and recordings which have the most tags none of which is among the selected tags are ranked to the bottom.

# Search #

The built-in search offered by Diktofon is **case-insensitive regular expression search**. This type of search can be used to locate character sequences in the transcriptions, and count and/or highlight the matches. It is not possible to locate transcriptions using a boolean search (such as: list all the transcriptions that contain both "Ansip" and "Laar" but not "Savisaar"). Also, the search is not aware of Estonian morphology.

If the search query consists only of letters and numbers, it behaves in the exact same way as the standard search provided by most text editors and web browsers. However, special symbols like brackets, dots, commas need to be "escaped" (i.e. preceded by a backslash) to stand for brackets, dots and commas, otherwise they perform a special function in the regular expression (e.g. a dot matches _any character_ rather that just a dot). Note that the transcriptions by nature contain very few non-letter characters.

## Examples ##

### Escaping ###

In order to count the sentences in a transcription you might want to search for the sentence-ending dot. In order to do that you have to escape the dot with a backslash, i.e. the query would be


```
\.
```

### Quantifiers and backreferences ###

To search for word repetitions (such as "ja ja" and "noh noh"), which are very common in spoken language, you can formulate the following query:

```
(\S{2,}) \1
```

This query matches all non-space sequences which are at least 2 characters long (`\S{2,}`) and which are followed by a space and then by itself (`\1`).

### Alternatives ###

To search or words which are either "laar", "ansip", _or_ "savisaar":

```
laar|ansip|savisaar
```

(Note that the simplest way of entering a vertical bar on HTC Wildfire (any pre v2.3 Android device?) is to use another computer to write yourself an email that would contain a vertical bar and then copy-paste it from the received email into the search box. ;( However, the HTC virtual keyboard contains the broken bar ¦, which Diktofon supports as an alternative to the vertical bar.)

### Phrase search ###

To search for a phrase, just enter it as it is (i.e. without quotation marks)

```
elas metsas mutionu
```

## See also ##

  * [Java class java.util.regex.Pattern](http://developer.android.com/reference/java/util/regex/Pattern.html)
  * [Vertical bar](http://en.wikipedia.org/wiki/Vertical_bar)


# Locale #

The language of Diktofon's user interface (i.e. text on buttons, labels, menu items) is either English or Estonian, and it depends on your phone's locale settings which language is used. If you want to set your phone's locale to Estonian but the built-in settings menu does not offer that option (like is the case on HTC Wildfire), then you can use a third-party app, e.g.

  * [MoreLocale 2](http://market.android.com/details?id=jp.co.c_lis.ccl.morelocale)
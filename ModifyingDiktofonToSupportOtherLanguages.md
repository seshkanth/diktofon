# Introduction #

Diktofon supports Estonian speech recognition. This document describes what kind of changes are needed to extend the support to other languages.

# How is speech-to-text performed in Diktofon #

Diktofon itself does not perform speech-to-text but delegates this to a webservice.

Diktofon assumes the following from the webservice

  * at least the _wav_ audio format is supported (because Diktofon's internal recorder can save only into _wav_)
  * speech recognition is performed in two steps
    * uploading the audio to a URL and (immediately) receiving an identifying token (short sequence of characters) as a response
    * downloading the transcription from another URL by specifying the token
  * the transcription is in the [Trans XML format](http://trans.sourceforge.net/)

Diktofon calls the webservice in `kaljurand_at_gmail_dot_com.diktofon.NetSpeechApiUtils.java`
which provides a wrapper around two (relatively simple) classes

  * `ee.ioc.phon.netspeechapi.AudioUploader`
    * input: audio file
    * output: String (token)
  * `ee.ioc.phon.netspeechapi.TranscriptionDownloader`
    * input: String (token)
    * ouput: Trans-formatted transcription

which are provided by the [net-speech-api](http://code.google.com/p/net-speech-api) project.

# Changes needed to support another language #

To add support to another language one must implement a compatible speech-to-text webservice for this new language and rewrite `AudioUploader` and `TranscriptionDownloader` to work with this new service. No changes are needed to the code of Diktofon (except for replacing `lib/netspeechapi.jar` with the updated version containing the modified `AudioUploader` and `TranscriptionDownloader`).
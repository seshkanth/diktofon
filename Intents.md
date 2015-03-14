## Introduction ##

Diktofon can communicate in various ways with the other apps installed on the device by using the Android intent-mechanism. The following provides a short overview.

## Incoming intents ##

The incoming intents allow other apps to summon Diktofon to perform a certain job for them. The incoming intents are declared in `AndroidManifest.xml` which describes precisely which activities respond to which intents. A short overview is:

  * record audio (RECORD\_SOUND)
  * search, e.g. using the Quick Search Bar (SEARCH)
  * share/send, i.e. push an audio file into Diktofon's collection (SEND)
  * **TODO**: PICK, i.e. pull an audio file from Diktofon's collection

## Outgoing intents ##

The outgoing intents allow Diktofon to summon other apps to perform a certain job. These intents are declared in the source files of the activity-classes (`app/src/kaljurand_at_gmail_dot_com/diktofon/activity/`) and have corresponding menus in the Diktofon UI.

  * record new audio using an external recorder (RECORD\_SOUND)
  * pull in an existing audio file from/using an external app (ACTION\_GET\_CONTENT)
  * share an audio file (and possibly its transcription) using email, social media, etc. (SEND)
# Sam, the Non-Binary TTS Voice

[Sam](https://bit.ly/36OjUbt) is a non-binary text-to-speech (TTS) voice that can be embedded into any voice assistant software solution. [Accenture Labs](https://www.accenture.com/us-en/about/accenture-labs-index) created Sam in collaboration with [Cereproc](https://www.cereproc.com/). By open-sourcing the components that we used to create this voice, we hope to encourage adoption and creation of others like it in the future so that there will eventually be a diversity of non-binary voices out in the world.

Inclusion and diversity are fundamental to Accenture's culture and core values. As such, we ask that usage of these assets is consistent with [Accenture's commitment to inclusion and diversity](https://www.accenture.com/us-en/about/inclusion-diversity-index) and compliant with Human Rights Laws and Human Rights Principles (as each is defined below).

> "Human Rights Principles" refers to the recognized principles of international human rights as defined in the United Nations Universal Declaration of Human Rights and the United Nations Global Compact.

> “Human Rights Laws” means any applicable laws, regulations, or rules (collectively, “Laws”) that protect human, civil, labor, privacy, political, environmental, security, economic, due process, or similar rights. Where the Human Rights Laws of more than one jurisdiction are applicable or in conflict with respect to the use of these assets, the Human Rights Laws that are most protective of the individuals or groups harmed shall apply.

Disclaimer: Some of the training audio used contains references to sex, gender, religion, and other potentially graphic or offensive content. This content does not represent the views of Accenture, Accenture Labs, or its employees.

## Table of Contents

+ [**Process Overview**](#process-overview)
+ [**Sam Creation Assets**](#sam-creation-assets)
+ [**Listen to Sam**](#listen-to-sam)
+ [**Trained models**](#trained-models)
+ [**Licensing**](#licensing)
+ [**Contacts**](#contacts)

## Process Overview

We started by selecting a voice over actor and recording 6 hours of audio from an open-source script. This data was pre-processed to lower the pitch to bring the pitch to the range between the average male and female speaker. This data was then used to train the acoustic prediction model for Sam.

We transcribed audio data from a separate non-binary speaker to train the prosody model, also pre-processing the data to increase the pitch to the same range. The prosody model is then used to "guide" the acoustic prediction model at synthesis time.

Future works could aim to transfer part of the non-binary voice quality to the acoustic model, or may involve using some voice over data in the prosody model training for an improved compatibility between both speech production models.

For more information on the full process, including related work, selecting a voice over actor, how the voice was refined with the non-binary community through surveys, and next steps, please see the information in the presentation folder.

## Sam Creation Assets

**Voice Over Recordings**

The Sam creation process began with the recording of base voice audio by voice talent [Mel Murphy](https://www.melmurphyvo.com/) (MM). All raw audio recordings can be found in the voice_over_recordings. There is a total of 6 hours of recording from the voice talent and a full ~8 hour script to accompany the recordings. The script contains all open source content.

**VO Voice Quality Transformation**

This audio was then transformed to sound more like a "non-binary speaker" by affecting two components: the voice quality and the speaking style of the voice. The underlying assumption here is that the acoustic cues of a non-binary voice are contained both in the prosody domain and the voice quality.

First the recordings were pre-proccessed by lowering the pitch of MM's audio by about 15%. This brings the pitch to the range "between" the average male and the female speaker. The pre-proccessed MM recordings were used to train the acoustic prediction model for Sam and can be found in the vo_voice_quality_transformation folder.

**Prosody Model Voice Data**

We then transferred a "non-binary" speaking style to the voice. This was done using a donor voice, [Avery Smith](https://www.blessedarethebinarybreakers.com/) (AS), and was chosen for their clear, consistent speaking style and for their natural mixture of masculine and feminine speech patterns and intonation. AS also had a large amount of publicly available audio that we could use. In total, we transcribed a total of 3.5 hours of audio from this speaker. The AS audio and the associated transcripts can be found in the prosody_model_voice_data folder. Due to the length of this audio, it is provided here in .mp3 format, rather than .wav like the voice over recordings.

**Prosody Model Voice Quality Transformation**

As this speaker has a lower pitch than our voice over actor, we raised the pitch of their audio by about 7%. Applying a voice quality transformation to both the MM and AS voices ensures they sound closer in pitch to one another. We trained the prosody model for Sam with the the transformed audio dataset from AS. The prosody model trained on AS data is used to "guide" the acoustic prediction model at synthesis time.

One of the challenges with this speaker and the small amount of data used was that the resultant TTS voice sounds more monotone than what is usually considered natural. The use of SSML markup is critical to making the voice sound natural and changing the emotion and intonation of the speech.

**Average Model Voice Data**

As both sets of data are rather small and in a single speaking style, the final models are "adapted" from average models incorporating data from dozens of male and female speakers, balanced so that the median of the pitch and vocal tract length distribution fall approximately to the average of male and female ranges. The adaptation procedure itself involves retraining specific layers of neural networks at different rates, to transfer certain characteristics of the average model to the final model, such as the ability to speak with different emotions and elocution styles.

To make the average models more robust for our purposes, we had individuals rate male and female speakers on a spectrum of gender perception. We also sourced, transcribed, and added voice data from a number of non-binary, trans, and intersex individuals, which significantly improved the resultant sound of the final TTS voice. The audio used from these individuals is all publicly available and the audio and associated transcriptions can be found in the average_model_voice_data folder.  

## Listen to Sam

You can hear generated audio samples of Sam in the folder sam_samples. The text used to generate these samples, including the SSML markup can also be found here.

## Trained models

 *[Idlak](https://github.com/Idlak) models and recipe coming soon*

## Licensing
These assets are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0.txt).

## Contacts

Andreea Danielescu\
​*Future Technologies, Accenture Labs*\
[andreea.danielescu@accenture.com](mailto:nonbinary_voice@accenture.com?subject=[GitHub])

​Lara Pesce Ares\
​*Technology Vision, Accenture Labs*\
​[lara.pesce.ares@accenture.com](mailto:nonbinary_voice@accenture.com?subject=[GitHub])

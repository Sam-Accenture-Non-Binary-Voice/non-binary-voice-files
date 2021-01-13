# Idlak documentation

## Running Idlak with pretrained models

### Setup

To save space and ensure you are using the latest version of the language resources it is required to link to the current Idlak data.
In general the following recipe would work, assuming you cloned idlak into `$HOME/idlak`. This only needs to be done once.

```
# location of this README file
MODELDIR=$( pwd )
# Idlak directory
IDLAKDIR=$HOME/idlak

cd $MODELDIR/vo_voice_quality_transformation/lang
ln -s $IDLAKDIR/idlak-data/en en
cd $MODELDIR/voice_over_recordings/lang
ln -s $IDLAKDIR/idlak-data/en en
```

### Synthesis

Once you have completed the setup above, you can run synthesis with the following commands:

```
SAMPLESDIR=$MODELDIR/../sam_samples/idlak
cd $IDLAKDIR/idlak-egs/tts_tangle_custom/s2
echo "This is a sample of TTS synthesis with the unmodified voice." | local/synthesis_voice_pitch.sh $MODELDIR/voice_over_recordings $SAMPLESDIR/voice_over_recordings
echo "This is a sample of TTS synthesis with the modified voice." | local/synthesis_voice_pitch.sh $MODELDIR/vo_voice_quality_transformation $SAMPLESDIR/vo_voice_quality_transformation
```
**NB: the output directory will be deleted, always use a new location**

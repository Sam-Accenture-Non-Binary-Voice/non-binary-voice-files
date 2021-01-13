# Idlak documentation

## Running Idlak with pretrained models

### Setup

To save space and ensure you are using the latest version of the language resources it is required to link to the current Idlak data.
In general the following recipe would work, assuming you cloned idlak into `$HOME/idlak`. This only needs to be done once.

```
# location of this repository 
NBVOICE=$HOME/non-binary-voice-files
# Idlak directory
IDLAKDIR=$HOME/idlak

MODELDIR=$NBVOICE/idlak_models
cd $MODELDIR/vo_voice_quality_transformation/lang
ln -s $IDLAKDIR/idlak-data/en en
cd $MODELDIR/voice_over_recordings/lang
ln -s $IDLAKDIR/idlak-data/en en
```

### Synthesis

Once you have completed the setup above, you can run synthesis with the following commands:

```
SAMPLESDIR=$NBVOICE/sam_samples/idlak
cd $IDLAKDIR/idlak-egs/tts_tangle_custom/s2
echo "This is a sample of TTS synthesis with the unmodified voice." | local/synthesis_voice_pitch.sh $MODELDIR/voice_over_recordings $SAMPLESDIR/voice_over_recordings
echo "This is a sample of TTS synthesis with the modified voice." | local/synthesis_voice_pitch.sh $MODELDIR/vo_voice_quality_transformation $SAMPLESDIR/vo_voice_quality_transformation
```
**NB: the output directory will be deleted, always use a new location**

## Training Idlak

Idlak tangle includes an example for training custom voices, rather than specific corpa.
These are the steps that were followed to create the models in this repository.

```
# location of this repository 
NBVOICE=$HOME/non-binary-voice-files
# Idlak directory
IDLAKDIR=$HOME/idlak

MODELDIR=$NBVOICE/idlak_models

cd $IDLAKDIR/idlak-egs/tts_tangle_custom/s2

# training with the original voice recordings
rm -rf voices/en/ga/mmu
./run.sh --spk mmu --lng en --acc ga --audio_dir $NBVOICE/voice_over_recordings --script_file $MODELDIR/text.xml --srate 16000
mkdir -p $MODELDIR/voice_over_recordings
cp -r voices/en/ga/mmu/*  $MODELDIR/voice_over_recordings/.

# training with the voice quality transformed voice
rm -rf voices/en/ga/mmu
./run.sh --spk mmu --lng en --acc ga --audio_dir $NBVOICE/vo_voice_quality_transformation --script_file $MODELDIR/text.xml --srate 16000 --stage -2
mkdir -p $MODELDIR/vo_voice_quality_transformation
cp -r voices/en/ga/mmu/*  $MODELDIR/vo_voice_quality_transformation/.

cd $MODELDIR/vo_voice_quality_transformation/lang
rm -r en
ln -s $IDLAKDIR/idlak-data/en en
cd $MODELDIR/voice_over_recordings/lang
rm -r en
ln -s $IDLAKDIR/idlak-data/en en
```





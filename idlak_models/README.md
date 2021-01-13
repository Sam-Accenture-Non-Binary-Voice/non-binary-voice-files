create symbolic link in model/lang to idlak-data/en
IDLAKDIR=$HOME/idlak
# from location of README file
cd vo_voice_quality_transformation/lang
ln -s $IDLAKDIR/idlak-data/en en
cd -
cd voice_over_recordings/lang
ln -s $IDLAKDIR/idlak-data/en en



# 3dprint-mri


3D print brain from .nii file start to finish

install freesurfer 7: https://surfer.nmr.mgh.harvard.edu/fswiki/rel7downloads, but can follow install and tutorial using page for version 6: https://surfer.nmr.mgh.harvard.edu/fswiki/rel6downloads
 
follow instructions and convert a sample (bert) into .pial files
 
then read gibhub page: https://github.com/miykael/3dprintyourbrain

set all environmental variables according to tutorial (see Setup and Configuration section below for variables to put in .bashrc file)
  
  export EXPERIMENT_DIR=/home/daniel/ubuntu/3dbrain
  export SUBJECTS_DIR=$EXPERIMENT_DIR/freesurfer
  export subjT1=$EXPERIMENT_DIR/${subject}/struct.nii.gz
  export subject=sub001

  export FREESURFER_HOME=/home/daniel/ubuntu/freesurfer/freesurfer
  source $FREESURFER_HOME/SetUpFreeSurfer.sh



take the already made .nii file from scanner (should be gzipped into a .gz file, if not, can zip it back via gzip <filename>)
  
put this .nii.gz file into directory: 3dbrain/freesurfer and rename it struct.nii.gz
  
proceed with making a surface model with freesurfer (see section below: “Step 2 - Create Surface Model with FreeSurfer”
 
  mkdir -p $SUBJECTS_DIR/${subject}/mri/orig
	mri_convert ${subjT1} $SUBJECTS_DIR/${subject}/mri/orig/001.mgz
	recon-all -subjid ${subject} -all -time -log logfile -nuintensitycor-3T -sd $SUBJECTS_DIR -parallel

this results in 2 files, lh.pial and rh.pial. These files should be made by freesurfer at 3dbrain/freesurfer/dan_brain/surf (according to step 3 on github page)
  
then follow step 3 on github page to concatenate the 2 hemispheres:
	mris_convert --combinesurfs $SUBJECTS_DIR/${subject}/surf/lh.pial $SUBJECTS_DIR/${subject}/surf/rh.pial \$SUBJECTS_DIR/cortical.stl
  
(will need to remember that I set subject=sub001 as dan_brain)
  
run cura to visualize (see below)
  
print brain at www.3dprinteros.com and sign in thru SSO → Duke
  
  
  

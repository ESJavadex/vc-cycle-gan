# Voice conversion by using CycleGAN  
### [Project Page](https://001honi.github.io/static/projects/vc-cycle-gan/vc_cycle_gan.html) follow this site for the result and more.
### Reference
Paper:<br>https://github.com/001honi/001honi.github.io/blob/master/static/projects/vc-cycle-gan/static/pdf/CycleGAN-VC-1711.11293.pdf<br>
Implementation:<br>https://github.com/leimao/Voice-Converter-CycleGAN
<hr>

### Changelog
As referenced above, we highly utilized from @leimao 's work while constructing this project. Google’s Colaboratory is used to train our model due to lack of high-performance GPUs. Some updates are required to reduce the time-consuming process as a main reason. The training for one model took approximately 5.5 hours after these updates with NVIDIA Tesla T4 GPUs. Two models trained for female-to-female and male-to-female voice conversion. Here is the detailed updates:
##### TRAINING
  - Training hyper-parameters, audio processing and default path variables are separated from related scripts; gathered together into 'hyparams.py'
  - 'decay_threshold' parameter is added for monitoring the learning rate reduction over iterations. 
  - In the reference implementation, iteration size dependent on the number of given training audio files not the length; therewithal, learning rate decays with iterations to converge to global minima. However, our dataset and file organization are different and old hyper-parameters result in stop of learning. Therefore, below figure is the plot of new learning rates for both generator and discriminator over growing epochs and iterations.
<p align="center">
  <img src="/figure/learn_rate.png" />
</p>  

##### PERFORMANCE
  - After realized the training per epoch is so slow because of model-saving and validation operations; 'check_epoch' parameter is added to control them. 
  - With the help of another if condition, epoch duration is decreased from approx. 55 seconds to 4 seconds. (Google Colab - NVIDIA Tesla T4 GPU)
  - Validation functions for conversion from B-to-A is removed. (We only need A-to-B)
##### FIX 
  - From now on, epoch range starts from 1 instead of 0.
##### MISCELLENOUS
  - All converted voices generated in validation are stored now; '-CONV-#-EPOCH' extension is added to converted voice filenames to observe the progress.
  - Elapsed time per epoch sensitivity is edited in the order-of-milliseconds.
  - Never-used scripts and folders are removed.

# Animation Autoencoder
Procedurally generate or interpolate between animations for a bipedal humanoid using a multi-pose autoencoder. TFlite is used within Unity to create animations in real time. The autoencoder is trained on animations from 3D content sites (e.g. https://www.mixamo.com/) and data captured from Azure Kinect Body Tracking SDK. Future encoders will be trained on data recorded from a curated list of videos after running a pose estimation algorithm. 

## Dependencies
- Python 3+
- Unity 3D
- Blender 2.7+

## Generate training data
- download a few animations from https://www.mixamo.com/ 
- put files in a directory and run the Blender script to extract 3D joint positions

## Create animations from videos
https://www.tensorflow.org/lite/models/pose_estimation/overview

Character animations are created from videos using a pose estimation algorithm

![](Figures/pose_example.gif)

17 joint positions are converted to a Unity/Blender compliant rigged character format

## Record data with an Azure Kinect

Use the Azure Kinect Body Tracking SDK within Unity to create a series of training samples

https://github.com/curiosity-inc/azure-kinect-dk-unity

![](Figures/dance_party.gif)

## Procedural Animations
17 joint positions with an x,y,z coordinate totals 51 features for the model. The inputs are encoded using a fully connected neural network into a latent space of 3 dimensions

![](https://miro.medium.com/max/1968/1*44eDEuZBEsmG_TCAKRI3Kw@2x.png)

A VR demo with hand tracking controls is used to explore the latent space and procedurally generate animations in Unity

Use a GAN to create animation paths in the latent space by pre-evaluating the space

Use the autoencoder to smooth real-time motion capture 

## Extracting data from a rigged character 
https://answers.unity.com/questions/1591435/animate-a-character-entirely-through-xyz-coordinat.html

https://docs.unity3d.com/Manual/UsingHumanoidChars.html

extract the position information from each child object of a rigged model

a minimum of 15 bones are required to produce a valid character model in Unity
https://docs.unity3d.com/Manual/class-Avatar.html

Tutorial on VAE: https://arxiv.org/pdf/1606.05908.pdf


Export Animations from Unity to FBX Ascii
https://www.youtube.com/watch?v=Hy2U0UYp6cA

http://ufldl.stanford.edu/tutorial/unsupervised/Autoencoders/

https://douglasduhaime.com/posts/visualizing-latent-spaces.html

https://medium.com/tensorflow/variational-autoencoders-with-tensorflow-probability-layers-d06c658931b7


Good references in: 
https://towardsdatascience.com/gans-vs-autoencoders-comparison-of-deep-generative-models-985cf15936ea

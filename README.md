# Cycle GAN for Image Transfer

The objective of this project is to train a cycle GAN that will be used to transfer image between day and night.

## Environment
* Tensorflow 2.4
* OpenCV
* PILLOW

## Concepts of Cycle GAN
The model architecture is comprised of two generator models: The image below shows a simple GAN architecture.

<img src="https://github.com/taimur1871/cycle_gan_tutorial/blob/main/images/simple%20cycleGAN.png" style="width:500px;height:500px;">

1. One generator (Generator-A) for generating images for the first domain (Domain-A)
2. Second generator (Generator-B) for generating images for the second domain (Domain-B).

In this case 
* Domain-A: Daytime
* Domain-B: Nighttime

### Generator Translations
* Generator-A -> Domain-A
* Generator-B -> Domain-B

The generator models perform image translation, meaning that the image generation process is conditional on an input image, specifically an image from the other domain. Generator-A takes an image from Domain-B as input and Generator-B takes an image from Domain-A as input.

Domain-B -> Generator-A -> Domain-A
Domain-A -> Generator-B -> Domain-B 
Each generator has a corresponding discriminator model.

The first discriminator model (Discriminator-A) takes real images from Domain-A (daytime images) and generated images from Generator-A and predicts whether they are real or fake. The second discriminator model (Discriminator-B) takes real images from Domain-B (night-time images) and generated images from Generator-B and predicts whether they are real or fake.

Domain-A -> Discriminator-A -> Real/Fake
Domain-B -> Generator-A -> Discriminator-A -> Real/Fake
Domain-B -> Discriminator-B -> Real/Fake
Domain-A -> Generator-B -> Discriminator-B -> Real/Fake

The discriminator and generator models are trained in an adversarial zero-sum process, like normal GAN models.
The generators learn to better fool the discriminators and the discriminators learn to better detect fake images. Together, the models find an equilibrium during the training process.

Passing an image through both generators is called a cycle. Together, each pair of generator models are trained to better reproduce the original source image, referred to as cycle consistency.

Domain-B -> Generator-A -> Domain-A -> Generator-B -> Domain-B
Domain-A -> Generator-B -> Domain-B -> Generator-A -> Domain-A

Our goal is to train such a 2 set Generator-Discriminator pair, to finally generate night-time images from day-time ones and quantify performance.

## Results
The images elow show translation from day to night and night to day for images in the dataset.
### Day to Night

<img src="https://github.com/taimur1871/cycle_gan_tutorial/blob/main/images/day-night.png" style="width:500px;height:500px;">

### Night to Day

<img src="https://github.com/taimur1871/cycle_gan_tutorial/blob/main/images/night-day.png" style="width:500px;height:500px;">

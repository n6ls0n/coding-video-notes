# Notes

Notes for <https://read.wiley.com/books/9781118711750/page/0/section/top-of-page>

## Table of Contents

- [Video Coding and Video Quality](#video-coding-and-video-quality)
  - [An Overview of Video Coding](#an-overview-of-video-coding)
  - [Inputs and Outputs](#inputs-and-outputs)
  - [Structural Elements](#structural-elements)
  - [Prediction](#prediction)
  - [Transform and Quantization](#transform-and-quantization)
  - [Bitstream Coding](#bitstream-coding)
  - [The Coded Bitstream](#the-coded-bitstream)
  - [Storing and Transmitting the Coded Bitstream](#storing-and-transmitting-the-coded-bitstream)
  - [The Decoder](#the-decoder)
  - [The Video Codec Model](#the-video-codec-model)
- [Structures](#structures)
  - [Coded Video_Sequence to Picture](#coded-video_sequence-to-picture)
  - [Coded Video_Picture to Basic Unit](#coded-video_picture-to-basic-unit)
  - [Coded Video_Basic Unit to Block](#coded-video_basic-unit-to-block)
  - [HEVC Coding Structures](#hevc-coding-stuctures)
  - [Structures In Versatile Video Coding_H266](#structures-in-versatile-video-coding_h266)
- [Intra Prediction](#intra-prediction)
  - [Introduction](#introduction)
  - [The Intra Prediction Process](#the-intra-prediction-process)
  - [Intra Prediction Modes](#intra-prediction-modes)
  - [Prediction Block Sizes](#prediction-block-sizes)
  - [Signalling Intra Prediction Choices](#signalling-intra-prediction-choices)
  - [Choosing a Prediction](#choosing-a-prediction)
  - [HEVC Intra Prediction](#hevc-intra-prediction)
  - [VVC Intra Prediction](#vvc-intra-prediction)
- [Inter Prediction](#inter-prediction)
  - [Inter Prediction - The Basics](#inter-prediction-the-basics)
  - [Forward Backward and BiPrediction](#forward-backward-and-biprediction)
  - [Inter Prediction Block Sizes](#inter-prediction-block-sizes)
  - [Motion Vectors](#motion-vectors)
  - [Sub-Pixel Interpolation](#sub-pixel-interpolation)
  - [Reference Pictures](#reference-pictures)
  - [Signalling Inter Prediction Choices](#signalling-inter-prediction-choices)
  - [Skip Mode](#skip-mode)
  - [Loop Filter](#loop-filter)
  - [When Inter Prediction Does Not Find a Good Match](#)
  - [HEVC Inter Prediction](#hevc-inter-prediction)
  - [Inter Prediction in VVC](#inter-prediction-in-vvc)
- [Transform and Quantisation](#transform-and-quantization)
  - [Residual Blocks](#residual-blokcs)
  - [Block Transforms](#block-transforms)
  - [Quantisation](#quantisation)
  - [Transform and Quatisation in Practice](#transform-and-quantization-in-practice)
  - [HEVC Transform and Quantization](#hevc-transform-and-quantization)
  - [Transform and Quantise in H266 Versatile Video Coding](#transform-and-quantise-in-h266-versatile-video-coding)
- [Entropy Coding](#entropy-coding)
  - [Entropy Coding for Video Compression](#entropy-coding-for-video-compression)
  - [Pre-processing](#pre-processing)
  - [Probability Models and Context Adaptation](#probability-models-and-context-adaptation)
  - [Variable Length Coding](#variable-length-coding)
  - [Arithmetic Coding](#arithimetic-coding)
  - [Binary Arithmetic Coding](#binary-arithmetic-coding)
  - [Context Adaptive Binary Arithmetic Coding](#context-adaptive-binary-arithmetic-coding)
  - [Entropy Coding in HEVC](#entropy-coding-in-hevc)
  - [Entropy Coding in H266_VCC ](#entropy-coding-in-h266_vvc)
- [Coded Video Filtering](#coded-video-filtering)
  - [Filtering and Video Coding](#filtering-and-video-coding)
  - [Detecting and Correcting Video Artifacts](#detecting-and-correcting-video-coding-artifacts)
  - [HEVC In-Loop Filtering](#hevc-in-loop-filtering)
  - [VVC Filtering](#vvc-filtering)
- [Storing and Transporting Coded Video](#storing-and-transporting-coded-video)
  - [Storing and Delivering Coded Video](#storing-and-delivering-coded-video)
  - [Coded Video File Formats](#coded-video-file-formats)
  - [Transport of Coded Video](#transport-of-coded-video)
  - [Video Rate Control](#video-rate-control)
  - [Error Handling](#error-handling)

### Video Coding and Video Quality

#### An Overview of Video Coding

- One second of original, uncompressed SD video, captured at 25 frames per second, takes up around 15.5 MBs of storage space. This means that the video clip would require 124 Mbits/second of bandwidth to transmit over a network or broadcast channel in real time, i.e. one second of playable video sent every second

- One seocn dof uncompressed UHD video captured at 50 frames per second, take sup around 620 Mbs of storage space and would require a substantial 5Gbit/seond of transmission bandwidth to send in real time

- A video codec is used to encode/decode video for storage and transmission

- It can be a software program, hardware module on a chip (integrated circuit), or a combination of the two

- The codec does a computationally intensive job which is to convert many millions of pixels per second to and/or from a compressed or encoded form

- The encoder carries out the basic following steps to create a compressed file:

  1. Partition: Decompose the video frame into basic regions, usually square or rectangular blocks of pixels

  2. Predict: For each region or block, create a prediction or an estimate of the block using information such as neighbouring pixels or previously coded frames. Subtract this prediction from the actual block to create a residual or difference block

  3. Transform and quantize: Transform the residual block into a frequency domain. Quantize the transformed block, which has the effect of discarding less-important components of data and retaining only the visually important features

  4. Entropy encode: Convert the result of the quantize step together with any other information needed to decode the frame into a compressed format

- The decoder then performs the reverse of the encoder steps to get the original video



#### Inputs and Outputs

#### Structural Elements

#### Prediction

#### Transform and Quantization

#### Bitstream Coding

#### The Coded Bitstream

#### Storing and Transmitting the Coded Bitstream

### Structures

### Intra Prediction

### Inter Prediction

### Transform and Quantisation

### Entropy Coding

### Coded Video Filtering

### Storing and Transporting Coded Video

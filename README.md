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

- A video encoder takes in uncompressed video and outputs a compressed (coded) bitstream. Other information may also go into the encoder such as parameters to control its operation and/or information to be embedded in the video bitstream

- The video decoder takes in a coded bitstream and produces uncompressed displayable video as its output. Further information such as status, timing and side information, may also be output

- A digital video camera captures a real-world image and converts it to a sampled form. The moving image is sampled at certain time instants to produces frames or fields of video

- A frame is a snapshot of the scene at a particular time instant and a field captures half the visual information in a frame, for example, the odd lines or even lines, at each instant

- Interlaced video which consists fo a series of fields is largely obsolete in 2023. Modern-day capture devices and displays record and show video as a series of complete, progressive frames at a particular number of frames per second, known as the video frame rate

- Each video frame is sampled usually on a rectangular grid, forming an array of pixels.A displayable pixel may be monochrome or color. A monochrome pixel can be represented with a single number indicating the brightness of the pixel. Larger values represent brighter pixels closers to white and smaller values represent darker pixels closer to black

- Video captured by a camera sensor or displayed on a screen may be in RGB format which menas that each captured or displayed pixel has a Red, Green and Blue component

- Red, Blue and Green are additive primary colors i.e. they can be mixed to produce a wide range of colors. Each of these can be represented as an N-bit number where N is an integer

- A complete image or video frame can be represented as three colour planes, each containing all the pixel values of the red, green ad blue components

- RGB is three-component system i.e. a colour pixel can be represented by a weighted combination of three components (R, G and B). Many other component systems can be used. A minimum of three components are required to represent full color

- YUV or YCrCb is a popular color space for image and video data. In this system, the luminance or luma component Y represents the brightness of each pixel position, corresponding to a monochrome version of each image or video frame

- The red component can be expressed as R = Y + Cr, where Cr is the red chroma or colour difference, representing the positive or negative difference between each luma sample Y and each Red pixel R

- Similarly, the blue and green component B = Y + Cb and G = Y + Cg

- A complete, in fact, overcomplete representation fo the image is Y, Cr, Cb, Cg

- Only three components are necessary to fully represent the image. The fourth component can be calculated by combining the other three. In the popular YCrCb format, the green chroma component Cg is omitted. An image can be converted from RGB to YCrCb or vice versa using a set of mathematical operations. Hence, images can be converted from one format to another without any loss in information

- One advantage of a colour space such as YCrCb is that human observers are less sensitive to colour than to brightness or luma. The chroma components (Cr and Cb) can be sub-sampled with respect to the luma component (Y) without having an obviously detrimental effect on image quality

- A video encoder makes many decisions while compressing a video sequence. Control parameters or values may be input to the encoder such as target bit rates or file sizes and information about the format of the video input. These parameters may be selected by the user, hardwired into the encoder application or device and/or calculated or derived automatically during encoding

- Along with encoding parameters, further side information may be passed to the encoder for embedding in the coded bitstream, such as text or metadata about what the video clip contains, information to help the playback device display the video and so on

- A video decoder may output statistics and other side information together with the decoded video

- A coded or compressed video is a sequence of bits. Encoded in this sequence is a complete compressed representation of the original video clip. The sequence of bits is put together in a specific way that is usually defined by a standard or a specification, such as High Efficiency Video Encoding (HEVC)/H.265 or AV1. When the structure of the coded video sequence matches the requirements of the specification and the video can be decoded according to the specification, we would say that it conforms to the specification or standard

- The coded sequence may be stored in one or more video or media files or it may be streamed or transmitted directly. The way the coded video sequence is organised for storaf=ge or transmission may itself be defined as part of one or more standards

#### Structural Elements

- An encoder or decoder handles the video data in a structured and organized way. The general approach is to break the video clip into a hierarchy of elements such as:
  1. Sequence: A complete video clip, scene or program, consisting of a series of frames

  2. Group of Pictures: A set of coded video frames, with the decoder having the ability to start decoding within the Group of Pictures

  3. Picture: A coded video frame that may be inter-related to other pictures in a Group of Pictures

  4. Slice or tile: A subset or a region within a picture. Each picture is split up or partitioned into one or more slices. Alternatively or perhaps simultaneously, the picture may be split into Tiles, eahc of which is a square or rectangular region of basic units. The H266/VVC standard introduces further partitioning, the subpicture

  5. Basic Unit (MG, CTUs or SuperBlock) : The basic unit of processing is typically a square region of video samples. IN older standards such as H264/AVC and MPEG-2, the basic unit or MB was set at 16x16 pixels. Formats such as H265/HEVC and AV1 cater for larger basic units of up to 64x64 pixels and the H266/VVC standards supports a basic unit size of 128x128 pixels. Larger basic units tend to be more effective compressing higher-definition content but can take more processing power and memory to encode or decode

  6. Block: The block is a square or rectangular region withing a basic unit and is a grouping of samples for prediction, transformation or processing

#### Prediction

#### Transform and Quantization

#### Bitstream Coding

#### The Coded Bitstream

#### Storing and Transmitting the Coded Bitstream

#### The Decoder

#### The Video Codec Model

### Structures

### Intra Prediction

### Inter Prediction

### Transform and Quantisation

### Entropy Coding

### Coded Video Filtering

### Storing and Transporting Coded Video

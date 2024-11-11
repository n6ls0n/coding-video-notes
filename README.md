# Notes

Notes for <https://read.wiley.com/books/9781118711750/page/0/section/top-of-page>

## Table of Contents

- [Video Coding and Video Quality](#video-coding-and-video-quality)
  - [An Overview of Video Coding](#an-overview-of-video-coding)
  - [Inputs and Outputs](#inputs-and-outputs)
  - [Structural Elements](#structural-elements)
  - [Prediction](#prediction)
  - [Transform and Quantization Process](#transform-and-quantization-process)
  - [Bitstream Coding](#bitstream-coding)
  - [The Coded Bitstream](#the-coded-bitstream)
  - [Storing and Transmitting the Coded Bitstream](#storing-and-transmitting-the-coded-bitstream)
  - [The Decoder](#the-decoder)
  - [The Video Codec Model](#the-video-codec-model)
  - [Video Codec Performance](#video-codec-performance)
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
- [Transform and Quantization](#transform-and-quantization)
  - [Residual Blocks](#residual-blokcs)
  - [Block Transforms](#block-transforms)
  - [Quantization](#Quantization)
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

- The purpose of compression is to reduce the number of bits required to store or send a video clip. A video clip is made up of multiple frames, each of which contains thousands or millions of pixels. Predicting each pixel in the frame makes it possible to reduce the information in the frame which in turn makes the frame easier to compressed

- Considering a single pixel in a video frame, the encoder creates a prediction pixel and subtracts it from the original pixel. The result is a difference or residual pixel. If the prediction is accurate, the difference is small or zero which means it contains less information that the original pixel

- It is possible to create a new prediction for every pixel. However, it can be more efficient to process a group of pixels at a time. A video codec may split each frame up into regions or blocks and process each block as a unit. For each block of original pixels or samples, the video encoder creates a prediction block and subtracts this from the original block to generate a residual block

- The encoder sends at least two things to the decoder namely a compressed version of the residual block and instructions for creating the prediction

- The decoder receives this information and then decompresses the residual block and creates the same prediction as the encoder by following the instructions previously sent. The decoder then adds the prediction block to the decompressed residual block to create a decoded block. By doing this for every block in the frame, the decoder reconstructs a complete video frame

- Usually the difference or residual block , when visualized, appears to have much less visual information than the original. Each sample in the residual block has a value that can be positive or negative

- Because the prediction block is reasonably similar to the original block, most of the residual samples are small positive or negative numbers, close to zero

- Small magnitude or zero samples are much easier to compress than the original pixel values

- For most of the pixels, the encoder should find a good prediction resulting in a residual frame that is usually a flat grey color which represents residual samples that are very close to zero

- In some areas of the frame, especially around the edges of moving objects, the prediction is not so good because the prediction pixels are not a good match fo the original pixels. In these areas, the residual samples have larger-magnitude positive (light grey) or negative (dark grey) values

- If we view the residual frame as a surface plot, we can see the positive and negative residual samples as peaks and troughs on the surface. The goal of the prediction process is to create a residual that is as close to possible to zero, subject to some other constraints

- The encoder has a number of choices for creating each prediction block. A video coding standard usually doesn't specify exactly how an encoder should choose a prediction. However, the Standard does set out the range of options available to the encoder. The Standard sets out the range of options for prediction and a video encoder decides how to create the prediction from within the range of options specified by the standard

- There are two factors to consider besides the desire to create an accurate prediction:
  1. How much information is required to tell the decoder hwo to create an identical prediction
  2. How much computation is required to generate the prediction?

- For every block in a video frame, the encoder can create a prediction block. The prediction block should be:
  1. A good match for the current block i.e. similar to the current block
  2. Created using the information that is already available to the decoder, so that the decoder can create the same prediction. This usually means that the prediction should be based on previously coded information
  3. Capable of being communicated to the decoder

- Predicting the block from pixels in the same frame is known as intra prediction. Predicting the block from pixels in a different frame is known as inter prediction

#### Transform and Quantization Process

- The output of the prediction process is a residual block, which is also the input to the transform and quantization process

- The transform process converts this block of residual samples into a block of transform coefficients. In itself, the transform does not remove or reduce information. Instead, it represents the block in a different form or domain

- The quantization process reduces the precision and the dynamic range of each of the transform coefficients. Quantization is a lossy process i.e. it removes information and is not reversible

- A two-dimensional transform converts a block of image samples into a block of transform coefficients. The transform coefficients represent the spatial frequency content in the original block of samples

- Each type of transform has its own set of basis patterns. Any image or residual block can be formed by weighting and combining or superimposing these patterns. The forward transform can be considered as a process that finds the weighting of each basis pattern required to form the image block

- An example of a 4x4 transform is the Discrete Cosine Transform (DCT). There are 16 samples in a 4x4 image block and there are 16 coefficients of the transform one corresponding to each of the 16 basis patterns

- The top-left pattern is a flat block, corresponding to zero frequency or 'DC'. Moving to the right, each pattern increases in frequency in the horizontal direction. Moving down, each pattern increases in frequency in the vertical direction. The lowest-right pattern is a checkerboard of horizontal and vertical frequencies

- Any 4x4 block of pixels or samples can be created by weighting and combining the 4x4 basis patterns. Different weights (i.e. coefficients) produce different blocks of samples when combining the patterns

- The transform does not compress data. Rather it represents the information from the original block in a form that may be more easily compressible

- Quantization reduces the precision of every coefficient in the block, which has the effect of setting small-valued or insignificant coefficients to zero. It is an irreversible or "lossy' process. The information removed during Quantization cannot be restored later

- The behavior of this process can be controlled by a quantization parameter which affects the strength of quantization. A larger QP results in more quantization i.e. greater loss of precision but also results in more compression

- QP is an important control parameter in a video codec because it has a direct effect on compression and quality

#### Bitstream Coding

- All the information necessary to decode the video sequence must be encoded i.e. packaged into a bitstream that is (1) compressed and (2) suitable for transmission and (3) decodable

- The information that needs to be sent may include:
  1. Quantized transform coefficients
  2. Prediction parameters, such as motion vectors, prediction mode choices, reference frame choices and prediction block sizes
  3. QP choice
  4. MB information
  5. Picture information
  6. Sequence information i.e. high-level parameters that affect the entire video clip

- First certain values are pre-processed i.e. converted into a suitable form for compression. Then, the processed values are entropy encoded i.e. coded into a compressed bitstream. Two commonly used forms of entropy coding are variable-length coding and arithmetic coding

- Preprocessing takes advantage of the statistical behavior of certain values produced by the video encoder

- Quantized transform coefficients tend to follow particular distributions. Typically, larger non-zero values are clustered around the top-left or DC coefficient with smaller or zero values towards the lower right or highest frequencies. The two-dimensional block of transform coefficients is converted to a one-dimensional array in a scanning pattern such as a zig-zig scan. The effect is generally to concentrate the significant non-zero coefficients together. This process is known as coefficient-reordering

- Prediction parameters and QP tend to be highly correlated amongst neighboring blocks in a coded frame. These parameters can be efficiently coded using differential prediction. For example, the encoder forms a predicted QP based on previously transmitted QP values. Instead of sending the QP itself, the encoder calculates and sends the difference between the predicted and actual QP. The decoder receives the differential value, forms the same prediction and adds the differential to the prediction to construct the QP. A similar approach can be taken for motion vectors, prediction modes and prediction block sizes, etc.

- After the pre-processing stage covered above, the original video sequence has been converted into a set of parameters and values sometimes described as symbols

- The entropy encoding process converts the symbols comprising a coded video sequence into an efficient binary form, a compressed bitstream. Basically going from base 10 to base 2

- Entropy encoding is a mapping between symbols and bits. There are different types of mappings such as:

  1. Fixed-length encoding: Each of the possible values of a symbol is represented with a binary code with the same number of bits, regardless of the value. THis mapping may be suitable for symbols that occur infrequently, e.g. a symbol that occurs once or only a few times per video sequence, such as a start-code or a sequence-level parameter. A fixed-length encoding is perhaps the simplest mapping but is not particularly efficient in terms of compression

  2. Variable-length encoding: A symbol is mapped to a binary code that may have a variable number of bits, depending on the value of the symbol. Typically, shorter binary codes are assigned to values that occur frequently (with a high probability) and other longer binary codes are assigned to values that occur less frequently (with a low probability). Variable-length codes may be structured, i.e. capable of algorithmic construction, such as the Exponential-Golomb (Exp-Golomb). Exp-Golomb codewords can be constructed according to a pattern: n leading zeroes, followed by a 1, followed by an n-bit binary word. An Exp-Golomb codeword can be constructed for any index value. Alternatively, variable-length codewords may be designed specifically for a particular value or set of values. For example, Context-Adaptive Variable-Length Coding (CAVLC) for transform coefficients in H264/AVC uses a mapping that is specific to the structure and values found in a block of transform coefficients. Variable-length codewords for video coding should be uniquely decodable so that there is no ambiguity in the value that is to be decoded. A limitation of variable-length encoding is that each symbol must be represented by an integral (whole) number of bits. In fact, the most efficient mapping for a symbol with probability of occurrence P is log2(1/P) bits, which may be a fractional number rather than an integer

  3. Binary arithmetic encoding: In an arithmetic coder each symbol is mapped to a range or interval so that a series of symbols can be represented by a fractional number. This fractional number is in turn mapped to a binary code. Arithmetic coding does not require each symbol be individually mapped to an integer number of bits. Instead, symbols are represented by a fractional number of bits, and as the number of symbols represented by a single number increases, arithmetic coding can approach the ideal mapping of log2(1/P) bits per symbol. In a practical video codec, several compromises are made when implementing arithmetic coding. General arithmetic coding, in which a symbol can take any one of multiple values, can be replaced with binary arithmetic coding, in which symbols are binarised i.e. converted into a binary representation, prior to encoding, such that the arithmetic coder only works on binary values. Computationally intensive multiplications or divisions can be replaced with approximations, and the range of potential values for each interval may be restricted in order to simplify processing

  4. Context adaptation: Variable-length encoding and arithmetic encoding rely on knowledge of symbol probabilities to provide maximum compression. Early video coding standards such as MPEG-2 and H263 used pre-determined probability tables derived from analysis of generic video sequences. More recently, H264 and HEVC employ context adaptation, in which symbol probabilities are adapted based on the actual statistics of the current video sequence. The video encoder and decoder measure the frequency of occurrence of symbol values and maintain a running total of the probability of each value occurring. Along with statistics from neighboring, previously coded values, these probability totals can be used to derive the codewords (VLC) or ranges (arithmetic coding)

#### The Coded Bitstream

- The coded video sequence consists of a hierarchy of parameters or syntax elements. At the sequence level, a header contains coded parameters that are necessary for decoding subsequent coded frames or pictures. Each picture may or may not have a header and may be made up of a number of slices, each of which corresponds to an area of the coded picture. Each slice is made up of a number of coded basic units such as MBs or Superblocks. Finally, each coded unit comprises header information, prediction parameters such as motion vectors or intra prediction modes, and coded transform coefficients

#### Storing and Transmitting the Coded Bitstream

- The coded bitstream is suitable for efficient storage or transmission

- In file storage, a complete coded sequence can be stored in a file. A media file containing compressed video is known as a container and may contain extra information such as a header, timing or synchronization parameters, one or more audio tracks and subtitles. These other data may be interleaved with the video information, so that the video file may be played by extracting and decoding video frames, audio chunks and associated information

- In network transmission, the coded sequence may be transmitted over a packet network such as the Internet. The sequence must be packetized i.e. split up and placed in network packets for transport. The syntax of a coded video sequence is typically designed to accommodate packetized transmission. For example, important header information such as sequence parameters may be sent in an initial packet and at regular intervals. Each slice or picture may be sent in a separate packet, or multiple slices may be sent in a packet. Resynchronization points (e.g. intra coded pictures that can be decoded in isolation from other data, are inserted at frequent intervals so that the clip can be played from random points and so that any transmission losses can be recovered)

- In broadcast transmission (which includes transmission over a broadcast medium such as cable, terrestrial or satellite TV) whats involved is the mapping of coded video and audio into a sequence of transmission packets, which is associated with a particular programme or channel. Transmission packets from multiple programmes are multiplexed together and carried via the broadcast medium. Issues such as random access, recovery from transmission errors and switching between channels or programmes are handled in a similar way to network transmission i.e. by inserting regular synchronization points in the coded sequence

#### The Decoder

- Decoding the compressed video sequence involves reversing the steps of the encoder

- An entropy decoder reads the compressed bitstream, parses the arithmetic, variable-length or fixed-length coded data and recovers the sequence of symbols that comprise the video sequence

- Pre-processing steps such as predictive coding and coefficient scanning are reversed. The decoder constructs the same predictors as the encoder e.g. motion vector predictors and uses these to recover the coding parameters. Decoded coefficients are inverse scanned to reconstruct blocks of quantized transform coefficients

- The reverse of the forward quantization process i.e. the quantization of transform coefficients carried out during encoding is rescaling

- It is often referred to as inverse quantization but it is important to note that it is not a fully reversible process. Because forward quantization removes information removes information, rescaling does not recover the original transform coefficients but instead produces a decoded set of coefficients with some loss of precision

- Transform coefficients that were originally low-valued and were set to zero by the quantization process will remain zero after rescaling. Other coefficients will be restored to their approximate magnitude but may have lost precision

- The inverse transform converts the block of decoded transform coefficients into a block of decoded images or residual samples. Because of the loss of information in the transform coefficients, the decoded image block will not be identical to the original image block

- The decoder creates the same prediction block or MB that the encoder created by generating a spatial or motion-compensated temporal prediction using the same prediction parameters - modes, motion vectors, etc as the encoder

- This prediction block is added to the decoded residual samples from the output of the inverse transform. The result is a decoded block or MB that can be displayed and/or used for further predictions

- As each MB is reconstructed and decoded, it can be places in its correct position in a decoded frame. Once a complete decoded frame has been built up, it is available for output and/or storing in a decoded frame buffer to form further predicted frames

#### The Video Codec Model

- Most mainstream video codecs have all adopted the same basic structure. The encoder applies the following steps to convert basic units e.g. a MB, 16x16 pixels into a compression bitstream:

  1. Motion compensated prediction from one or more previously coded frames and/or intra prediction from previously coded samples in the same frame

  2. Subtraction of a motion-compensated prediction from the current basic unit to form a residual unit, such as a residual MB

  3. Block transform and quantization to form blocks of quantized coefficients

  4. Entropy encoding of quantized coefficients and side information such as motion vectors and headers

  5. Rescaling (inverse quantization), inverse transform and addition of motion-compensated prediction to reconstruct a local copy of the decoded frame or field

- The decoder carries out the following steps to convert a compressed bitstream into a decoded sequence of frames or fields:

  1. Entropy decoding to extract quantized coefficients, motion vectors and headers

  2. Rescaling and inverse transform to form a residual unit

  3. Motion compensated prediction and addition of the prediction to the residual

#### Video Codec Performance

- Most present-dayt codecs for consumer applications use lossy video compression, which means that the decoded video is not identical to the original video. Typically, the encoder introduces this loss during the quantization process. Once the visual data has been quantized, the lost data cannot be restored

- The performance of a video codec i.e. how good it is at compressing video, can be evaluated along three dimensions:

  1. Compression or rate: How much is the video compressed by? How much space do I need to store the compressed video file? What bitrate do I need to transport the compressed video?

  2. Computation: How complex is the process of encoding or decoding? Can I encode or decode in real time on a particular processor? How much memory e.g. RAM, do I need during encoding or decoding? How much power does the encoding or decoding consume?

  3. Quality or distortion: How does the decoded video look? DOes it look indistinguishable from the original i.e. visually lossless? Are there obvious distortions such as blockiness or blurring? Does the decoded video look smooth or jerky? Is the quality good enough for the application?

- When comparing video codecs or determining whether to include a proposed modification during the development of a video coding standard, it is common practice to measure the rate-distortion performance. This involves comparing the decoded video quality across a range of compressed bitrates

- The relationship between quality and coded bitrate is known as a rate-distortion curve

- A better codec or codign method will tend to produce higher-quality decoded video across a range of bitrates

- It is often the case that better-rate distortion performance comes at a cost of higher computation at the encoder, decoder or both\

- Bitrate or compressed file size is relatively easy to measure simply count the number of encoded bits per second of the video i.e. encoded bitrate or the number of bytes in the encoded video file. Computation can be measured or estimated for example by counting the seconds it takes to encode a complete video file

- However, visual quality is a different matter because the question of 'how good does this video look?' is fundamentally a subjective question

- We cannot fully measure or predict how a human observer will assess the quality of a video

- We can approximate or estimate a visual quality in several ways, which can be categorized as subjective or objective methods

- One popular subjective test is the double stimulus continuous quality scale (DSCQS) method

- A popular objective quality measure is the Peak signal-to-noise ratio. It is expressed in decibels, where a higher number implies better visual quality

  $$PSNR_{db} = 10 \cdot \log_{10} \left(\frac{(2^n - 1)^2}{MSE}\right)$$

- It is a simple calculation and has been widely used to estimate the quality of compressed versus original video images

- The PSNR metric suffers from several limitations. PSNR requires an unimpaired original image for comparison but this may not be available in every situation. PSNR does not correlate particularly well with subjective video quality measures such as ITU-R 500. For a given image or image sequence, high PSNR usually indicates high quality and low PSNR usually indicates low quality. However, a specific value of PSNR does not equate to an absolute subjective quality. PSNR and similar metrics are adequate for comparisons of different encodings of the same video sequence but not necessarily adequate for comparisons across different video materials

### Structures

### Intra Prediction

### Inter Prediction

### Transform and Quantization


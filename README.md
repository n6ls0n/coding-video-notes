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
  - [Coded Video_Sequence to Picture](#coded-video-sequence-to-picture)
  - [Coded Video_Picture to Basic Unit](#coded-video-picture-to-basic-unit)
  - [Coded Video_Basic Unit to Block](#coded-video-basic-unit-to-block)
  - [HEVC Coding Structures](#hevc-coding-structures)
  - [Structures In Versatile Video Coding H266](#structures-in-versatile-video-coding-h266)
- [Intra Prediction](#intra-prediction)
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
  - [When Inter Prediction Does Not Find a Good Match](#when-inter-prediction-does-not-find-a-good-match)
  - [HEVC Inter Prediction](#hevc-inter-prediction)
  - [Inter Prediction in VVC](#inter-prediction-in-vvc)
- [Transform and Quantization](#transform-and-quantization)
  - [Residual Blocks](#residual-blocks)
  - [Block Transforms](#block-transforms)
  - [Quantization](#quantization)
  - [Transform and Quantization in Practice](#transform-and-quantization-in-practice)
  - [HEVC Transform and Quantization](#hevc-transform-and-quantization)
  - [Transform and Quantize in H266 Versatile Video Coding](#transform-and-quantize-in-h266-versatile-video-coding)
- [Entropy Coding](#entropy-coding)
  - [Entropy Coding for Video Compression](#entropy-coding-for-video-compression)
  - [Pre-processing](#pre-processing)
  - [Probability Models and Context Adaptation](#probability-models-and-context-adaptation)
  - [Variable Length Coding](#variable-length-coding)
  - [Arithmetic Coding](#arithmetic-coding)
  - [Binary Arithmetic Coding](#binary-arithmetic-coding)
  - [Context Adaptive Binary Arithmetic Coding](#context-adaptive-binary-arithmetic-coding)
  - [Entropy Coding in HEVC](#entropy-coding-in-hevc)
  - [Entropy Coding in H266 VCC](#entropy-coding-in-h266-vvc)
- [Coded Video Filtering](#coded-video-filtering)
  - [Filtering and Video Coding](#filtering-and-video-coding)
  - [Detecting and Correcting Video Artifacts](#detecting-and-correcting-video-artifacts)
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

- One second of uncompressed UHD video captured at 50 frames per second, take sup around 620 Mbs of storage space and would require a substantial 5Gbit/seond of transmission bandwidth to send in real time

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

- The behavior of this process can be controlled by a quantization parameter (QP) which affects the strength of quantization. A larger QP results in more quantization i.e. greater loss of precision but also results in more compression

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

- A complete video clip or sequence is processed by a video encoder to create a compressed bitstream. In order to handle the large amount of image data in a sequence of video frames, the encoder splits it up into manageable structures

- A coded video sequence is a series of coded pictures that, when decoded, will play back as a complete video clip. Coded frames or pictures may be organized into multi-picture structures during encoding such as Group of Pictures

- Each picture may be coded as a single unit or in multiple sections known as slices or tiles. Each slice or tile contains one or more Basic Units such as Macroblocks or Coding Tree Units

- The Basic Unit is a unit of data handled by the encoder and decoder

- In present-day codecs, it is square

- In the older MPEG-2 and H.264/AVC standards, it is 16 x 16 pixels, up to 64 x 64 pixels in the H.265/High Efficiency Video Coding (HEVC) standard and up to 128 x 128 pixels in the H.266/VVC standard

- The Basic Unit may be split into smaller blocks for processing steps such as prediction and transformation

- Early video codecs had limited processing and storage capacity and so processing was applied to small regions such as 8 x 8 blocks

- Memory and processing capacity have improved significantly since then but nevertheless a codec breaks a sequence down into progressively smaller regions for processing

- A complete sequence is divided or partitioned into groups of coded frames or pictures then into individual coded frames then regions within a frame then square or rectangular blocks

- A typical video scene is made up irregular-shaped regions with varying textures, colors and movement behavior. This does not correspond neatly to a regular block-based structure.

- A codec attempts to model and predict the behavior of the video sequence, which implies that irregular structures might produce better compression efficiency

- However, irregular or changing structures need to be communicated to the decoder, whereas a fixed or repetitive structure can often be inferred and may not require to be communicated

- For example, if the Macroblock size is fixed at 16 x 16, there is no need to communicate the size from the encoder to the decoder

- There is a trade-off between using structures such as fixed-size code blocks versus structures that can change size and perhaps shape. Fixed-size blocks are simple to process and do not require many bits to communicate the structure to the decoder, but they may be a poor match to the actual video content

- Structures that can change size and shape may be capable of more accurately reflecting actual video content, but they may be more complex to process and require a significant number of bits to communicate

- Most practical codecs make a compromise, which allows a certain amount of variation in the structures whilst basing the structures on rectangular or square blocks

- Assuming we have a coded video frame with an overlay of prediction block structures. The encoder would choose between a range of square and rectangular block sizes in order to optimize compression of regions with different amounts of detail

- In a relatively homogenous area, the encoder could choose a larger block size such as 64 x 64

- In complex moving areas, the encoder could choose smaller block sizes that more closely follow the movement and object boundaries

- A coded video sequence is stored and transmitted before decoding and playbakc. Transmission over a network requires an efficient mapping between the coded bitstream and network packets.

- Other challenges include:
  1. Supporting random access so that a user can join part-way through a clip or navigate to a suitable playback point rather than always having to start from the beginning of the sequence

  2. Streaming playback, achieving a compromise between good playback quality and avoiding stalling and rebuffering

  3. Handling errors so that a lost packet or corrupted section does not ruin playback of the entire clip

#### Coded Video Sequence to Picture

- A coded video sequence may correspond to a video clip, a programme or a section of a programme. In addition, a coded sequence may include parameter sets, which are coded structures that contain the common parameters that are needed for decoding and that apply to multiple coded pictures

- For example, an H264 or H265 Sequence Parameter Set (SPS) contains parameters that are common to an entire coded sequence. A Picture Parameter Set (PPS) contains further parameters that are common to one or more pictures in a coded sequence

  - Assume we have a coded sequence. One SPS contains the decoding parameters for the entire coded sequence. The first PPS inherits some common parameters from the SPS and includes further decoding parameters

  - In order to decode slices of coded video, a decoder needs parameters from the SPS and the currently active PPS

  - A single encoded video frame is a coded picture or a coded frame. Decoding a coded picture should produce a complete, displayable video frame. Pictures or frames may be coded without prediction from other pictures or frames using intra-coding and/or with prediction from other pictures or frame using inter-coding

  - Pictures or frames may be grouped into multi-picture structures. For example, random access to a video sequence requires an independently decodable picture such as an intra-coded picture and it is common to insert intra-pictures at intervals in a sequence

  - In many applications of video encoding, coded pictures are organized as Groups of Pictures (GoP) where each GoP contains an intra-coded picture followed by a number of inter-coded pictures

  - This can make it easier for a user to join a video stream part-way through or to switch to an earlier or later part of a video clip - a process known as random access - and/or recover from transmission errors by seeking to the next intra-coded picture

- A sequence is a series of coded frames or pictures representing a complete video. This could be for example a programme, a clip or a scene. Picture or frames in the sequence will typically have common characteristics such as:
  1. Spatial Resolution e.e. Standard Definition, High Definition or other resolutions
  2. Frame rate
  3. Color Depth and Color space
  4. Coding parameters such as Profile, Level and CU size

- Pictures in the sequence may be arranged with certain structural relationships. For example, a GoP is a repeating, multi-picture structure consisting of intra-coded picture or I-picture, with a number of inter-coded pictures. The inter-coded pictures could be P-pictures, in which each block is predicted from one frame or B-pictures in which each block is predicted from two frames

- While the coded frames are typically intended for playback and display, a coded sequence may include non-displayed coded data such as:
  1. Parameter sets: These are coded data structures containing information that may be common to multiple coded pictures in the sequence such as the common characteristic above
  2. Redundant frame: These may contain redundant picture data that are not intended to be displayed unless the main or primary pictures are lost or damaged
  3. Non-displayable reference frames: These are pictures that may be used for prediction but are not intended for display, such as automatically generated reference frames or background scene elements

- A coded picture is a complete compressed frame or a field or pair of fields in the case of an interlaced video sequence

- It may be made up of multiple section such as slices and/or tiles. Parameters required to decode the picture may be coded in a header such as a picture header, in parameter sets and/or in one or more slice headers. A coded picture may have one of a number of types or characteristics such as:
  1. Intra-coded or I-picture: The picture is coded without any prediction from other coded pictures using intra-only prediction
  2. Inter-coded, P or B-picture: The picture may be coded using prediction from one (P) or more than one (B) previously coded pictures
  3. Used or not used for prediction: The picture may be used or not used for inter prediction of further coded pictures
  4. Resynchronization: The picture triggers a reset of coding parameters at the decoder and can be used as a resynchronization point
  5. Access/splicing point: The picture is intended to provide an access point for joining or splicing video clips together

- Coded pictures in a video sequence may be arranged in multi-picture structures. The early MPEG-1 and MPEG-2 standards introduced the concept of GoPs which historically consisted of an I-picture followed by a series of P or B pictures

- Recent standards such as H264 , HEVC and VVC have introduced considerable flexibility in multi-picture structures

- Such structures can serve a number of purposes including:
  1. Improved compression efficiency by enabling an encoder to make efficient use of multiple reference pictures
  2. Limiting decoding delay by restricting the number of pictures that need to be decoded before any given picture can be completely decoded and displayed
  3. Providing resynchronization points by including I-pictures at regular intervals

#### Coded Video Picture to Basic Unit

- A coded picture is a compressed representation of a single video frame or a coded field or pair of fields for interlaced video. In standard-based video codecs, a picture is processed in Basic Units such as MacroBlocks or Coding Tree Units

- The Basic Unit usually has a fixed size within the coded picture

- The choice of Basic Unit is a compromise: a larger size may be more efficient for representing larges areas of low detail in frame but requires more memory and processing power, whereas a smaller size may be more computationally simpler but less efficient for compression

- Each picture is arranged as a regular grid of Basic Units

- The Basic Units within a picture may themselves be arranged into structures such as Slices and/or tiles

- A slice is a series of Basic Units in a raster scan order and slices may contain an irregular number of Basic Units

- A tile is a square or rectangular structure containing multiple Basic Units

- Slices and/or Tile may be useful for:
  1. Mapping coding video data to transmission packets, for example, by sending each slice in a seperate network packet
  2. Handling errors, for example, resynchronizing at the start of the next error-free slice or tile
  3. Parallel processing, which would involve processing multiple slices or tiles simultaneously for faster encoding or decoding

- Each coded picture is made up of a series of Basic Units. A Basic Unit is a regular-sized square region. It's terminology varies from standard to standard:
  1. Macroblock: A Basic Unit consisting of 16 x 16 luma samples and associated chroma samples, used in VP8 H264 and older standards
  2. Supermacroblock: A Basic Unit consisting of 64 x 64 or 128 x 128 luma samples and associated chroma, used in VP9 and AV1
  3. Coding Tree Unit: A Basic Unit consisting of N x N array of luma samples and associated chroma. IN H265/HEVC, N can be 16, 32 or 64 and is set at the sequence level via SPS. In H266/VVC, N can range from 32 to 128

- An encoder has to process and store all the data and parameters of a Basic Unit. A larger Basic Unit requires more computational power and more local storage and so a smaller Basic Unit may be more suitable for decoder with low processing capabilities

- A certain number of parameters must be coded for each Basic Unit, unless the Basic Unit is skipped i.e. not coded. It may be more efficient to minimize the number of Basic Units in a frame by using a larger Basic Unit size. Furthermore, the Basic Unit is typically the larger possible partition size for prediction and coding so a larger Basic Unit gives more flexibility in assigning block sizes to regions of the frame

- Larger Basic Units can give better compression efficiency than smaller Basic Units can for high-resolution video e.g. HD and UHD/4K resolutions. This is because image features such as foreground and background objects are likely to take up a relatively larger number of pixels in a high-resolution video frame

- A picture may be coded as one or more slices, each of which is a contiguous series of Basic Units. Usually the picture is divided into a set of slices in a raster scan order from top left to lower right. Each slice contains an integral number of Basic Units and the end of one slice is immediately followed by the beginning of the next slice

- An encoder can use slices as a way of mapping coded data into packets or units for storage or transmission, for example, with each slice transmitted in a separate network packet

- If a packet is lost or corrupted, decoding can restart at the beginning of the next slice,,albeit with potential problems if other slices or pictures are predicted from the lost slice

- Prediction and inherited parameters may be restricted across slice boundaries

- An encoder may choose a fixed size for each slice, for example, a single slice per picture, or a fixed number of Basic Units per slice

- A potential disadvantage of fixed-size slices is that the amount of coded data per slice may vary considerably can can depend on whether the slice contains stationary background regions that are easy to predict or fast-moving foreground regions that are hard to predict

- This means that a picture coded with a uniform number of Basic Units per slice may result in coded slices with a significant variation in coded size. It may be preferable to choose slice sizes to maintain a roughly constant coded slice

- Increasingly, video codecs are handling larger frame sizes such as HD, 4K and above. Modern processors can contain multiple core capable of operating in parallel

- Video can be decoded quickly and more efficiently if multiple sections of a coded frame can be decoded simultaneously by multiple processing cores and/or multiple processing threads

- A picture may be coded as one or more tiles. Unlike slices, which may or may not be rectangular, tiles are always rectangular

- A coded picture is partitioned into regular equally sized tiles which can be square or rectangular
- During encoding, certain operations such as intra prediction, filtering and prediction mode signalling may be constrained so that there are no data dependencies across tile boundaries.

- This means that a decoder can process multiple tiles in parallel, decoding each tile without waiting for data in another tile to be decoded

- Constraining encoding dependencies in this way may cause a loss of compression efficiency as some prediction choices will not be available for Basic Units next to a tile boundary

- However, splitting a frame into regular-sized tiles that can be independently decoded makes it possible to decode large frames efficiently in parallel which has the potential to increase decoding speed and efficiency

#### Coded Video Basic Unit to Block

- The basic unit of coding in a standard-based video codec is a Macroblock or Coding Tree Unit. Each basic unit may be split or partitioned into structures for coding, prediction and transformation

- A video codec handles image data in units of square or rectangular blocks

- How big should these blocks be?

- The answer may depend on the size and content of each video frame. It may be more efficient to code the moving sections of the frame with smaller blocks and code the more static portions using larger blocks

- Early codecs adopted a one-size fit all approach fixing the basic unit size - the Macroblock size - at 16 x 16 pixels and the basic transform block at 8 x 8 pixels. However the best coding unit (CU) might depend on the content of the frame

- Later H264 introduced some flexibility with a fixed basic unit size - a 16 x16 Macroblock - but with flexible choices of block size for prediction and transform

- H265/HEVC and VVC have extended this flexibility and allowed the CU size to vary depending on the local scene content

- In HEVC, a fixed size Coding Tree Unit (CTU) may be partitioned into multiple CUs with varying sizes

- The fixed-size CTU allows a decoder to know exactly how much processing power and local storage are required to handle each CTU whereas the varying-size CU makes it possible to adjust the CU size depending on image content

- Pixels or samples are grouped into prediction areas such as Prediction Units (PUs) each of which is predicted by using previously coded data such as neighboring areas using intra-prediction or previously coded frames using inter-prediction

- Prediction areas are typically square or rectangular blocks

- All the samples in a PU are predicted in the same process

- Codecs such as H264, HEVC, and VVC support flexible choices of PU sizes and types

- Choosing the prediction structure involves questions such as:
  - How good is the prediction? In other words, how accurately does the prediction match the pixels or samples in the block
  - How many bits does it take to encode the choice of PU?
  - How many bits does it take to encode the type of prediction and parameters such as prediction mode and motion vectors

  - PUs are usually square or rectangular blocks with dimensions that are powers of 2, making it relatively easy to signal the size and shape of the block with a minimal number of bits

  - HEVC, an inter-predicted PU can be square or rectangular with certain specified dimensions

  - Each HEVC CU can be split into one or more PUs and also into one or more TUs. Some CUs may be partitioned differently for prediction and transformation

  - Signalling the prediction parameters for each PU may require a significant number of bits. Neighboring PUs often have similar parameters, such as motion vectors, reference frame choices and prediction modes, which can be used to reduce the number of bits required to signal prediction choices to the decoder

- After prediction, blocks of residual samples are transformed, quantized and encoded

- The size and shape of the region that is transformed, the Transform Unit (TU), affect compression performance

- As with PUs, larger or smaller TUs may each be suitable of different areas of a frame. A larger TU size may be more efficient for homogenous areas where all the residual samples in a large area share similar characteristics. This tends to be the case for areas of low detail and/or uniform texture such as smooth background regions

- A smaller transform size may be more suitable for detailed areas and/or where there is complex motion

- HEVC makes it possible to split each CU into another quadtree, this time for the purpose of specifying transform units (TUs)

- Each TU is a square region of samples that are transformed and quantized

#### HEVC Coding Structures

- A HEVC is stored or transmitted as a sequence of network access layer units (NAL units or NALUs)

- In this standard, a sequence would begin with parameter sets, each containing common decoding parameters that a decoder uses in the decoding of the coded video data. Each coded video frame or picture is sent as a series of one or more video coding layer (VCL) NAL units, each of which contains a coded slice segment. The slice segment can be decoded to generate the sequence of decoded video frames

- HEVC Parameter Sets are used to communicate coding parameters that may be common to many or all of the pictures in a video sequence

- Each parameter set may be encoded in its own NAL unit i.e. it is coded as a separate structure from the pictures in the sequence

- Parameter sets cna be sent as part of the coded bitstream or they may be communicated or defined separately and loaded as part of an agreed initialization sequence, without actually transmitting the parameter set from encoder to decoder

- The following are the HEVC Parameter Sets:
  1. Video Parameter Set (VPS): THis may be sent once at the start of a coded sequence or communicated 'out of band'. For example, a decoder could use a VPS that is pre-defined in the decoder software. Most of the parameters in the VPS relate to scalable or multiview coding and can be ignore for non-scalable coding with a single video layer. The Profile and Level discussed further below can be specified in the VPS and/or in the SPS

  2. SPS: This is sent once at the start of the coded sequence for non-scalable coding or communicated out of band. The parameters in the SPS are common to all the coded pictures in the sequence and include:
      - VPS identifier, referring to the VPS in use for this sequence
      - Profile and Level identifiers, as part of the profile_tier_level syntax structure
      - SPS identifier, a number in the range of 0 to 15 that identifies this SPS. PPSs use this identifier to indicate the inherited SPS
      - Spatial and temporal resolution
      - Color space format, 4:2:0, 4:2:2 or 4:4:4
      - Coding Tree Block (CTB) size, either 16 x 16, 32 x 32 or 64 x 64 luma samples
      - Minimum CB size
      - Minimum and maximum TB sizes
      - Enable or disable certain coding tools such as sample adaptive offset (SAO) filter and pulse code modulation (PCM) mode\
      \
      SPS parameters place certain requirements on the decoder such as the ability to handle a particular frame size, color depth and CTU/CTB size. Such requirements may be determine whether or not a particular decoder is capable of decoding this sequence. For example, a decoder with the ability to handle only 8-bit samples can determine whether the sequence is within its capability by parsing the SPS
      \
      Sending these parameters just once in the SPS means that they do not need to be re-sent during the video sequence, which minimizes the overhead in the coded

  3. Picture Parameter Set (PPS): The PPS contains parameters that may be common to some or all of the pictures in a sequence. Once a PPS has been received by a decoder it is available for activation i.e. for use in decoding. each coded slice refers to one PPS identifier, and all slices in a picture must use the same PPS. The PPS parameters include:
      - SPS identifier, indicating the SPS in use for this sequence
      - PPS identifier, a number in the range of 0 to 63 identifying this PPS. Coded slice can refer to any PPS that has already been received or is already available at the decoder
      - Enable or disable certain decoding features, such as dependent slices, sign data hiding, Context Adaptive Binary Arithmetic Coding (CABAC) initialization per slice, transform skip and weighted prediction
      - Initialize the quantization parameter (QP) for each slice using this PPS
      - Number of active reference prediction for inter-prediction
      - Wavefront parallel processing (enabled or disabled), using the flag entropy_coding_sync
      - Multiple tiles enabled or disabled. If enabled, the tile widths and heights are specified in the PPS
      -Parameters controlling the behavior of the in-loop deblocking filter
      - Merge mode parameters, used in inter-coding
      \
      In general, the PPS contains parameters that may be common to multiple pictures thus reducing overhead, but that may have to change during a coded sequence. For example, an encoder may choose to switch to a different default QP at some point during the coding

  4. Parameter Set Activation: Each slice header contains a PPS identifier. When a given PPS is referred to in a slice header for the first time in a sequence, thr PPS is activated and is then used for that slice and any further slices in the same coded picture. When an SPS is referred to in a PPS for the first time in a sequence, the SPS is activated. When the VPS is referred to in an SPS, the VPS is activated. When a slice is decoded referring to a different PPS identifier, the old PPS is deactivated and the new PPS is activated

- Profiles and Levels specify certain restrictions on the coded bitstream in terms of the features and algorithms that may be in use and also the range of values that a decoder might encounter

- A HEVC bitstream contains an identifier of a Profile and Level in the SPS and an HEVC decoder can use this to determine whether it has the capability to actually decode the bitstream

- A Profile indicates which subset of the HEVC features and algorithms may be present in the coded bitstream

- A Level indicates maximum ranges of certain values that a decoder may encounter in a coded bitstream. Each Level defines a maximum number of luma samples per second, a maximum Coded Picture Buffer Size, a maximum number of slice segments, a maximum number of tiles per picture and a maximum coded bitrate. Each Level from 1 to 6.2 effectively limits the data rate and video resolution that a decoder can encounter. A HEVC decoder that has the computational capability to handle a certain level should also be able to handle every level below

- HEVC's Reference Picture Set (RPS) can be used to signal repeating picture structures. The classic GoP, introduced in the early MPEG standards, consists of an I-picture together with a number of P - and/or B-pictures

- The RPS enables this and other structures to be efficiently communicated to the decoder

- In an HEVC bitstream, the inter-dependencies between coded pictures are captured by RPS entries for each picture, which indicate the choice of the reference picture(s) as an offset relative to the current picture

- The RPS is usually arranged as a temporal hierarchy of layers with the pictures with more dependencies (needing more neighboring pictures to be predicted) higher up in the hierarchy and vice-versa

- A decoder can decode all the pictures to produce a full frame rate output sequence or it can discard one or more layers, starting at the uppermost layer to produce a lower frame rate output with less decoding processing

- The decoder needs to know the complete list of reference pictures for each current picture. Communicating this for every picture may be expensive in terms of coding overhead

- In practical scenarios, RPSs often repeat, which means that the RPS for picture N can be used again for picture N + M at some point in the future

- Using HEVC, an encoder can specify a limited number of RPSs in the SPS

- Individual coded pictures or slices refer to one of these RPSs. This means that it is not necessary to send a complete specification of reference pictures for every picture. Instead, the encoder only needs to communicate an index identifying a pre-existing RPS

- In the older H264/AVC standard, random access in supported using instantaneous decoder refresh (IDR) pictures. HEVC extends this concept, introducing random access points and associated leading pictures

- As the name suggests, decoding of an HEVC stream can start at a random access picture (RAP)

- An RAP contains only intra-coded slices, so it is sometimes described as an intra-RAP

- There are three types of RAP: IDR, clean random access (CRA) and broken link access (BLA)

- The difference between these RAP types related to the use of leading pictures. A trailing picture is a picture that is coded only using prediction from previous pictures in display order

- A picture that is predicted from an RAP, which is sent after the RAP in coding order but precedes the RAP in display order, is a leading picture

- There are two types of leading pictures, decodable and skipped, denoted as random access decodable leading (RADL) picture and random access skipped leading (RASL) picture

- RADLs are coded without any prediction from reference pictures prior to the IRAP in coding order whereas RASLs can be coded using prediction from reference pictures that are older than the IRAP

- For RAP types in HEVC, an IDR picture clears the decoded picture buffer. This effectively means that the IDR starts a new video sequence. With an IDR, RADL-leading pictures may be allowed, depending on the NAL unit type, but RASL-leading pictures are not allowed. A CRA picture does not clear the decoded picture buffer, and RADL and/or RASL-leading pictures are allowed. A CRA is changed to a BLA during a splicing operation which causes RASLs to be ignored and skipped during decoding

- For non-RAP types in HEVC, the associated RAP is the most recent RAP in the coding order. A trailing picture is coded and displayed after the associated RAP. A leading picture is, RADL or RASL, is coded after the RAP but displayed before it. RADL or RASL pictures can use the RAP and any pictures that do not refer to pictures coded before the RAP as a prediction source. RASL pictures can use the RAP and pictures coded before the RAP as a prediction source. The use of RASLs can be beneficial to compression efficiency since some pictures can have extra prediction references and therefore more opportunities to create an optimal prediction but can introduce some complexity

- RAPs can facilitate random access and error recovery. As with many features of HEVC, it is up to codec designers how they use RAPs. Random access occurs when a user joins a video stream part-way through

- Decoding and playback can start at any RAP. If it is an IDR picture, decoding starts with the IDR and proceeds as normal.

- If it is a CRA picture, decoding starts with CRA itself. Any leading pictures are coded after the CRA picture but are intended to be displayed before the CRA picture

- RADL pictures may be successfully decoded because they do not depend on any earlier pictures. However RASL pictures depend on earlier reference pictures that mau not exist in the decoded picture buffer, so the decoder will discard the RASL pictures

- Similarly is an error occurs such as one or more lost packets, a decoder may restart decoding at the next RAP. Once again, RASLs will typically be discarded since they may depend on missing or errored older reference pictures

- A RAP will normally be encoded as an IDR or CRA picture. WHen two separate coded sequences are joined together or spliced, say in video editing session, the video editing software may use an IDR or CRA as a suitable starting point to start the second sequence

- If the splice point starts with a CRA picture the editing process may change its designation from CRA to BLA

- Leading pictures may be left as they are to avoid the need to adjust the coded bitstream. Note that changing from a CRA to a BLA picture merely involves replacing the nal_unit_type of each NAL unit associated with the picture. There is no need to partially or fully decode any pictures

- Any RASLs associated with the BLA may not be successfully decodable since they depend on reference pictures prior to the splice point that no longer exists. A decoder encountering a BLA in a coded video sequence should therefore ignore any RASLs associated with the BLA i.e. those coded immediately after the BLA which means that a certain number of the original video frames might not be displayable. RADLs can be successfully decoded

- For HEVC Coded Pictures, there is no separate picture header in the bitstream. Instead, what is sent is a series of one or more slice segments, each comprising a slice segment header and slice segment data

- Each slice segment in picture shares the same POC Value PicOrderCntVal and refer to the same PPS. When a decoder identifies a new POC in a slice, this indicates that the slices is part of a new picture

- The slice segment data consists of a series of CTUs. Each CTU is decoded and reconstructed in the appropriate position within the slice segment and if tiles are in use within the appropriate tile

- H265/HEVC introduces the concept of slice segments. These can be considered as a mechanism for subdividing slices into smaller segments and/or a way to reduce the size of the headers for each of a collection of slice segments

- In HEVC, a slice consists of one independent slice segment, with a complete slice header, followed optionally by one or more dependent slice segments, which each inherit some header syntax values from the independent slice segment

- Predictions cannot cross slice segment boundaries as a CB/CU in one slice segment cannot be predicted from a CB/CU in a different slice segment

- For intra-prediction, this means that samples outside of the current slice segment cannot be used to predict the current CB/CU and the prediction mode cannot be predicted based on blocks outside the current slice segment

- For inter-prediction, this means that prediction parameters cannot be predicted from outside the current slice segment

- For example, motion vectors predicted using Merge mode or Advanced Vector Prediction (AVMP) mode cannot be predicted from outside the slice segment. Loop filtering may or may not cross slice segment boundaries, depending on the parameter choice

- Each picture is coded as a series of slice segments. Slice segments can be useful for packetization e.g. sending each slice segment in a separate network packet without the overhead of sending a full independent slice segment header in every packet. However, if the decoder encounters an error it will need to wait for the next complete slice header i.e. the next independent slice segment to obtain all the parameters necessary to continue decoding

- An independent slice segment starts with a complete slice header, containing all the parameters necessary to decode the slice. Each dependent slice segment starts with a slice segment header that inherits some of its parameters from the slice header

- All slice segments start with a section that includes a few basic parameters such as the PPS identifier and the slice segment address, indicating the position if the first CTU in the slice within the picture, in raster scan order

- An independent slice segment header also includes a section which contains all the syntax elements that are necessary for decoding a slice

- Tile entry points may optionally be included. These are pointers that enable the decoder to process tiles in parallel

- After the slice segment header, the slice data consist of series of CTUs in raster order

- If both the independent and dependent slice segments are used within a coded picture, a series of dependent slices inherit parameters from the preceding independent slice segment header until a new independent slice is received

- In HEVC, the use of tiles is signalled with the tiles_enabled_flag in the PPS. If the flag is 1, the tiles are present in each picture which means that there may be more than one tile per picture, and the PPS further defined the number of tile rows and columns and indicates whether rows and columns are uniformly spaced

- If not uniformly space, the width of each row or column is explicitly signalled

- When each CTU in a picture is decoded, it is reconstructed in the appropriate place within a Tile. IN a similar way to slice segments, inter and intraprediction cannot cross tile boundaries. Loop filtering may or may not cross tile boundaries depending on the PPS. This makes it possible for the tile to be decoded in parallel

- CTUs in a tile with more neighbors may end up being compressed more efficiently due to this fact

- In HEVC, slices and tiles may coexist in a coded sequence and withing a coded picture. The restriction is that one or both of the following must be true:
  1. All CTUs in a slice segment belong to the same tile and/or
  2. All CTUs in a tile belong to the same slice segment

- It may be beneficial to parallelize the decoding of a coded picture, for example, using multiple processors or processing cores to speed up the time taken to decode a complete picture

- Parallel decoding at the picture level involves allocating certain decoding operations to different processors. Depending on the encoding choices, this may be done in a number of ways when decoding a HEVC sequence

- Recall, that tiles within a coded picture may be decoded in parallel. The following features of HEVC tiles make them suitable for parallel processing:
  1. Tiles are rectangular and may have a regular size. Having a regular and therefore predictable tile size may be helpful since each tile contains the same number of CTUs and should therefore be decoded using approximately the same amount of processing resources
  2. Predictions do not cross tile boundaries so decoding one tile does not necessitate waiting for another tile to be decoded
  3. For each tile in a slice segment or some of the tiles. an encoder may optionally insert an entry point marker in the slice segment header. In this scenario, each marker specifies the offset in bytes to the start of a tile in the coded bitstream. This allows each decoding process to start decoding a tile at the appropriate point without having to wait for the entire picture to be entropy decoded

- Each slice segment in an HEVC bitstream can be decoded somewhat independently, for example, by sending each slice segment to a different processing code for decoding. This may be less straightforward than parallel decoding of tiles, for example for the following reasons:
  1. Slice segments are not constrained to have a fixed or regular (CTUs per slice segment), so the processing time per slice may be unpredictable
  2. Dependent slice segments cannot be decoded until the associated independent slice segment is decoded since the dependent slice segments require the header information of the independent slice segment
  3. Unlike tiles, each slice segment has an associated header, albeit a small one for dependent slice segment so using multiple slice segments purely for the purpose of parallel decoding may be inefficient

- An optional HEVC feature sometimes described as enables parallel decoding of rows of CTUs, signalled by entropy_coding_sync_enabled_flag in the PPS

- If the flag is 1, then each row of CTUs may be decoded in parallel with certain conditions. First, the slice segment header contains an entry_point_offset for some or all of the rows of CTUs in the slice segment. Each offset indicates the offset in bytes to the start of the row of CTUs in the coded bitstream. Note that this is the same entry_point_offset mechanism used for tiles. Second, CABAC entropy coding is constrained so that each successive CTU row can be decoded after two CTUs from the previous row have been decoded. This works by:
  1. When encoding or decoding each row of CTUs, the entropy coding state or context state is stored after the second CTU in the row
  2. When encoding or decoding each row of CTUs after the first row, the entropy coding state of the first CTU in the current row is initialized with the entropy coding state of the second CTU in the previous row

- This entropy coding synchronization mechanism enables each row of CTUs to be decoded in parallel. The restriction is that each successive row has to wait for the entropy coding state to be stored for the previous row, so each decoding process can start one two CTUs in the row above have been decoded

- In real time, this produces a ripple or wavefront effect as the parallel decoding processes start for each row

- A decoder needs to know the size of the basic unit of coding i.e. the standard unit of coded picture data that it handles as it processes each frame

- In previous standards, this was a 16 x 16 pixel Macroblock. HEVC introduces the CTU with a size of 16 x 16, 32 x 32 or 64 x 64 set in the SPS and fixed for the duration of the sequence

- The CTU size places a bound on the computational requirements of a decoder. By setting the CTU size to maximum of 64 x 64 pixels, the decoder can be designed with the appropriate amount of memory and processing capacity to handle this amount of data per CTU

- The CTU comprises luma and chroma Coding Tree Blocks. For example, a 64 x 64 pixel CTU corresponds to one CTB of 64 x 64 luma samples and two CTBs of 32 x 32 chroma samples, assuming the sampling format is 4:2:0

- Whilst the CTU size is fixed for an entire HEVC video sequence, the CU can vary from CTU to CTU

- CTUs can be split into CUs of varying size

- The CU corresponds to a square block of pixels and can take any value between the minimum and maximum sizes defined in the SPS. Each CU comprises luma and chroma Coding Blocks (CB)'

- In an HEVC codec, the CTU is split into CUs using quadtree partitioning. A quadtree splits a block such as a square CTU or CU into four quadrants, with the option to continue to recursively split each quadrant

- At each level of the quadtree, a single-bit flag, split_cu_flag can indicate split or no split for each square. This makes a quadtree an efficient way to adapt the size of coding block or CU while minimizing the number of bits required to signal how the block is split

- A further optional partitioning of the CTU is into one or more Quantization Groups (QG). A Quantization Group is a multiple of CU size and effectively makes it possible for an encoder to group together multiple CUs for the purpose of signalling and calculation QP. Within the QG, delta QP i.e. the change from the previously signalled QP is sent at most once and so all the CUs share the same predicted QP

- In HEVC, every CU is partitioned into one or more prediction units (PUs) and one or more transformation units (TUs). Each PU contains luma and chroma Prediction Blocks (PBs) and each TU contains luma and chroma Transform Blocks (TBs). PU and TU partitioning in HEVC are not required to exactly match each other

- Each HEVC CU is coded using intra or inter prediction. A CU coded in intra-mode can be treated as a single i.e. the PU is the same size as the CU or split into four square PUs because the HEVC intra prediction modes operate on square blocks

- A CU coded in inter-mode can be split into two or four PUs in a number of ways, including square and rectangular PUs

- For both intra and inter prediction, a CU is split once at most into PUs. It is not a recursive process, unlike the partitioning into TUs

- Each PU is predicted using a set of parameters, an intra prediction mode for an intra-PU or an inter prediction mode plus further parameters such as motion vectors, reference picture index or indices, and merge index for an inter-PU

- An HEVC CU is partitioned into one or more TUs using another recursive quadtree structure known as a transform tree. Starting at the CU, at each level of the transform tree except for the lowest possible level, a flag is sent in the bitstream, split-transform_flag

- If the flag is 0, the tree is not divided further, if it is 1, the tree is split into four transform tress each with half the original CU horizontal and vertical dimensions. The process continues until either all flags are 0 or the tree has reached the lowest level and has been split to the lowest allowable level. The TUs themselves are the leaves of the quadtree. Each TU in a colour video sequence comprises a luma TB and two chroma TBs

- The number of levels allowed in the transform tree depends on the maximum and minimum TU size and the maximum transform tree depth, all of which are specified in the SPS. Possible TU sizes in HEVC range from 32 x 32 down to 4 x 4

#### Structures In Versatile Video Coding H266

- While it is not backwards compatible with HEVC, the newer VVC standard builds on many of the concepts of HEVC. Some of the structures in VVC are natural extensions of those found in HEVC, whilst others are actually simplifications of the HEVC approach

- VVC specifies s, SPSs and PPSs in a similar way to HEVC. In addition, the adaptation parameter set (APS) signals picture or slice parameters such as loop filter parameters that may change frequently from one slice or picture to the next, but which would be inefficient to signal with PPSs

- Repeating picture structures such as GOPs are signalled in VVC in a somewhat simpler way to HEVC but still with the capability to signal the reference picture arrangement for a GOP flexibly and efficiently

- Random access and bitstream splicing are supported in a similar way to HEVC with some simplifications. The concept of Gradual Decoding Refresh (GDR) is introduced in VVC in which a decoder can begin decoding at an inter-coded frame rather than an intra-frame, such that a correct decoded picture is gradually built up at the decoder over time

- VVC specifies a picture header that applies to all slices in a coded picture, a concept that existed in older standards such as H263 but was missing from H264 and HEVC. Syntax elements in the picture header do not need to be signalled again at the slice header level

- The slice concept is redefined. Slices in VVC comprise either rectangular slices, which are each a rectangular region that is an integral number of tiles or a rectangular subset of a tile or raster slices each comprising complete tiles in raster order. A new structure, the subpicture, defines a rectangular region of the picture that may contain one or more slices

- The Basic Unit, the CTU, can be up to 128 x 128 samples in size, compared with the maximum 64 x 64 sample CTU in HEVC and the maximum transform size is 64 x 64

- A CTU is partitioned into CUs, first using a quadtree in a similar way to HEVC then one or more binary splits and/or ternary splits

- Each of the leaf nodes of this partitioning process is a CU. CUs can thus be square or rectangular with a minimum size of 4 x 4 samples

- In most cases, the CU block size is also the block size used for prediction and transformation, so there is no separate PU or TU partitioning. VVC transforms can also be square or rectangular, matching the size and shape of each CU

In a CTU in an I-picture, luma and chroma may optionally be partitioned separately. The luma and chrome components of the CTU do not have to use the same partitioning into CUs

### Intra Prediction

- Intra prediction is the process of creating a prediction block based on pixels in the same frame as the current block

- Raster Order means left to right and top to bottom

- Intra prediction involves predicting a current block from nearby previously coded pixels in other blocks such as pixels above and/or to the left of the current block. Some or all of these pixels may be available in previously coded blocks

- There are three types of intra-prediction types:
  1. Flat or DC: All samples have the same prediction value, for example, the average value of adjacent pixels. The prediction block is a flat region with all the samples the same
  2. Planar: Samples are predicted by fitting a plane function to adjacent pixels. The prediction block is a gradient, with a smooth progression in value depending on the plane function
  3. Directional or Angular: Samples are predicted by extrapolating adjacent pixels in a particular direction; in this example, extrapolating diagonally down and to the right

#### The Intra Prediction Process

- The process of intra prediction in a video encoder is as follows:
  1. The encoder selects a prediction mode and creates a prediction block based on previously coded samples such as the samples above and to the left of the current block
  2. The prediction block is subtracted from the current block to create a block of residual samples
  3. The residual block is encoded and sent in the compressed bitstream along with the encoded prediction mode
  4. At the decoder, the residual block is decoded. This happens via the decoder using the prediction mode to create an identical prediction block to the one that the encoder created from the previously decoded samples in the same video frame
  5. The decoder adds the prediction block to the residual block and reconstructs the decoded current block

#### Intra Prediction Modes

- For an N x N sample block in a video frame, we want to form a prediction from neighboring,  previously coded samples. In general, some or all of the samples adjacent to the current block may be available as prediction sources. These include:
  - The sample at the top-left corner of the block
  - N samples immediately above the block
  - N samples above and to the right of the block
  - N samples immediately to the left of the block, and
  - N samples below and to the left of the block

- If these samples have already been coded by the time the encoder processes the current block, then they are available for prediction

- The encoder chooses a prediction for the current block based on a set of intra prediction modes defined in the coding standard and on the available samples above and to the left of the model. There are3 prediction modes:

  1. DC Prediction: This creates a prediction by calculating an average i.e. mean of the samples immediately to the left of the current block. This average value is copied into all samples of the current block. This mode works well when the current area of the frame is relatively flat and there is not much variation in the texture of the current block. If the top samples are not available, for example, if this is a block in the top row of the frame, then the prediction may be created by averaging only the left-hand samples. Similarly, if the left samples are not available, the prediction may be created by averaging only the upper samples. If neither left nor upper samples are available, for example, for the first, top-left block of an intra-coded picture, the prediction may be set to a constant value.

  2. Planar Prediction: This calculates a gradient function based on certain adjacent samples. It is less effective for detailed blocks

  3. Directional Prediction:  This creates an intra prediction by extrapolating or copying samples next to the block. Each type or mode of prediction relates to a specific direction. An encoder may attempt to predict the block with each of the available prediction modes and pick the mode that minimizes the energy in the residual block as long as this mode doesn't take too many bits to signal

#### Prediction Block Sizes

- When creating an intra-prediction , an encoder may be capable of choosing between a number of block sizes according to the limits set out in the standard. In general, a larger block size is best for regions of the video scene containing smooth texture or simple, strong details since a large block size will give reasonably accurate intra prediction and will cost the fewest bits to signal to the decoder

- A small block size may be better for regions with complex details. Smaller prediction blocks generally give a more accurate prediction but require more bits to signal the prediction mode of each block in a video frame, since there are more prediction blocks per macroblock or CTU and therefore more prediction modes to be signalled

#### Signalling Intra Prediction Choices

- For every prediction block, the encoder must communicate the choice of prediction mode. This typically involves encoding a parameter in the bitstream and sending it along with each coded block residual

- If the encoder selects a smaller prediction block size in an effort to improve prediction accuracy, the number of prediction modes communicated per frame increases

- Each intra prediction mode and each coded residual occupy space in the bitstream. The encoder should choose an intra prediction for each block that reduces the size of the coded residual. At the same time, the encoder should code the prediction mode using as few bits as possible

- H264 introduced the concept of coding the most probable intra prediction mode. As with many other aspects of video coding, it is a reasonable assumption that the mode of the current block is likely to be the same as or similar to the mode of previously coded blocs in the same area of the frame

- In an H264 codec, the most probable mode is taken to be the same mode as the last block that was coded using intra prediction. The MPM takes the fewest bits to code. If the actual choice of mode for this block is different, then we need to signal the actual prediction mode

#### Choosing a Prediction

- For each block of a video frame, the encoder has to choose a prediction mode. This can be a computationally demanding problem when there are many different modes and multiple block sizes to choose from. If enough computing resources are available, if encoding speed is not an issue and/or if the encoder has plenty of computational power, the encoder do the following:

  ``` cpp
  For each possible prediction block size {
        For each prediction mode {
              Calculate the number of bits to code the residual
              Calculate the number of bits to code the
               prediction mode
    }
  }
  ```

- The encoder chooses the combination of block size(s) and modes the produce the minimum number for encoded bits

- Assuming a current N x N sample block. It can be intra-predicted as a single block or as four N/2 x N/2 sample blocks. THe encoder tests every possible prediction mode for the N x N sample block size and notes the minimum number of bits required to code the mode and the residual. The encoder tests every prediction mode for each of the four N/2 x N/2 sample blocks and records the minimum number of bits required to code each mode and residual. THe final choice is the combination of block size and prediction mode(s) that gives the smallest total number of bits.

- Depending on the number of available prediction modes, it may not be possible for the encoder to fully test every possible combination of block size and mode. In practice, a video encoder may simplify the process of choosing a prediction mode by selecting a subset of available modes to test.

#### HEVC Intra Prediction

- H265/HEVC  intra prediction creates a prediction for the current prediction block (PB) from neighboring samples to the left and above the current PB

- An intra prediction block is square block of luma or chroma samples that can range in size from the CTU size, a maximum of 64 x 64 samples down to 4 x 4 samples

- Recall, the CTU is partitioned into coding units (CUs) that are made up of coding blocks (CBs). Each CB in an intra-coded CB is partitioned in PBs according to the following rules:
  1. If the CB is larger than the smallest allowable CB size, the PB is same size as the CB
  2. If the CB is smallest allowable size CB size, which is defined in the sequence parameter set as 8x8 or larger, the PB may be either the same size as the CB or split into four quadrants of 4 x 4 samples or larger. The choice of whether to split the CB is signalled with a flag in the bitstream

- HEVC supports 35 intra prediction modes. Mode 0 is planar prediction, mode 1 is DC prediction and modes 2 - 34 are directional or angular prediction modes

- Planar prediction, mode 0, fits a plane surface to the block. The surface is created by interpolating between four pixels, two above and two to the left of the current block

- DC prediction, mode 1, calculates an average of the above and left pixels and applies this average value across the entire block

- HEVC's 33 directional or angular prediction modes can be applied to intra-predicted PUs up to 32 x 32 in size. Each mode creates a prediction by extrapolating across the block of neighboring samples above and/or to the left

- The modes are chosen in such as way as to reflect that video content usually has more vertical and horizontal features than diagonal features

- When predicting a particular sample using an angular prediction mode, the prediction source may lie exactly on boundary sample position in which case that sample is used as the prediction source. However in many cases, the prediction source lies between boundary samples

- For larger prediction block sizes, 8 x 8 or larger, boundary samples are smoothed using a three-tap linear filter for certain prediction modes. The intra prediction is constructed by extrapolating from the smoothed boundary samples

- At slice or tile boundaries, some of the neighboring samples may not be available. The encoder may copy available neighboring samples into unavailable positions, making it possible to use a wider number of possible prediction modes in these situations

- The boundaries of predicted sample blocks are filtered to smooth discontinuities across block boundaries in certain situations, when the block is 16 x 16 or smaller and when certain prediction modes are selected

- HEVC codes the intra prediction mode of each PB based on the observation that neighbouring blocks tend to have the same or similar intra prediction modes. The encoder signals the decoder to use either a MPM from a list of three likely candidates or to use a specific mode that is not on the candidate list

- In luma prediction mode signalling, a list of three candidate prediction modes, the MPM list, is constructed depending on the intra prediction modes of neighboring previously coded blocks to the left and above. Any unavailable neighbors e.g. blocks that were coded using inter prediction rather than intra prediction, are set to DC mode. If both neighbors have the same directional prediction mode, then the MPM candidates are set to that mode, plus or minus one.

- In chroma prediction mode signalling, for each chroma PB, the encoder signals that the chroma PB should either use one of the planar, DC, horizontal or vertical modes or use the same intra prediction mode as the corresponding luma PB.

- The chroma components of a CU have a limited number of choices of intra prediction mode. Both components can inherit the luma prediction mode, or they can both be coded using modes 0 (planar), 1, (DC), 10 (horizontal), 26 (vertical) or in certain cases 34 (diagonal‐down)

#### VVC Intra Prediction

- Intra prediction in the VVC standard extends many of the concepts of HEVC intra prediction, providing more intra prediction options at the cost of increased computation. Enhancements include the following:
  1. Intra Prediction Modes: VVC adds 32 further directional modes to HEVC's 33, giving a total of 65 directional modes. A square block is predicted by extrapolating neighboring samples according to one of the prediction direction. Some of the angular modes are modified for the prediction of non-square blocks. Along with DC and planar modes, this gives a total of 67 possible intra prediction modes for each CU

  2. Intra Prediction of Rectangular Blocks: VVC coding units can be square or rectangular with aspect ratios of 1:1, 1:2, 1:4 or greater. HEVC only supports the intra prediction of square blocks, whereas any of the rectangular VVC coding units can be intra-predicted. When predicting a rectangular block using directional prediction, the default set of prediction directions may not be ideal. Instead, the directions are remapped. This allows the remapped modes to more provide effective coverage of all the directional angles that are likely to appear ina block of with these dimensions

  3. Intra Interpolation Filters: The interpolation filter used in HEVC intra prediction is extended to four taps from two and applied depending on the directional prediction mode

  4. Cross-Component Prediction: VVC supports 8 prediction modes for chroma blocks, including 3 modes based on chroma prediction from luma. Luma and chroma components of a block often have structural similarities. VVC introduces cross-component modes for chroma prediction. For these modes, after predicting the luma block, the reconstructed luma block is down-sampled and used to predict the chroma components. The prediction is formed based on the correspondence between edge pixels in the chroma and luma components. A prediction model is generated based on the similarity or difference between the edge samples of the luma and chroma blocks. Based on this model, the reconstructed luma block is used to create an intra prediction for the chroma block

  5. Extra Reference Lines: Intra prediction in HEVC and the earlier H264/AVC standards used reconstructed samples from the lines of samples adjacent to the current block. VVC supports the use of two further reference lines: Line 1, which is one sample removed from the current block and Line 3, which is three samples removed from the current block. The encoder can signal the selected reference line and the block is predicted using directional modes only from reconstructed samples in the selected line

  6. In VVC, intra-predicted luma blocks may be divided into two or four horizontal or vertical sub-blocks prior to carrying out intra prediction. Smaller blocks are divided into two partitions, and larger blocks are divided into four partitions. This process has the effect of breaking up intra prediction processed for larger blocks and increasing the opportunities for parallelization

### Inter Prediction

- Inter prediction is the process of creating a prediciton block based on pixels a different frame from the current video frame.

- Recall that for each block of pixels in the current video frame, it is often possible to find a similar block of pixels in a different video frame

- Inter prediction creates a prediction block based on previously coded pixels in a different video frame. This could be the frame just before the current frame i.e. one frame in the pad t, the frame just after - one frame in the future, or an older previous frame or newer future frame

- These are the options we can use to predict a block in the current frame:
  1. We can use the most recent frame as our prediction source
  2. We cna use an older frame as our prediction source
  3. We can use a future frame as our prediction source
  4. We can make a prediction by combining data from two or more frames, for example one from the past and one from the future

- The encoder deocdes or reconstructs each coded frame and creates inter predictions from these previously coded reference pictures. The encoder sends the residual, which is the difference between the prediction and the actual frame data, together with instructions so that the decoder can create an identical prediction

- The decoder stores deocded frames and uses theses as reference pictures. It uses the instructions send by the encoder to create thr same prediction as the encoder

- This means that the video encoder and video decoder maintain the same set of reference pictures and create identical predictions

- The frame or frames chosen as the source fo the prediction must be available at the decoder. This means that it is usally necessary to compress and send the prediction source frame(s) before the sending the current frame. This in turn measn that if the encoder uses the future frames as prediction sources, it must reorder the frames in the bitstream so that the decoder recieves these future frames before the current frame

#### Inter Prediction The Basics

- Assuming we are predicitng from the previous frame in the video sequence, for every blokc in the current frame (N), the encoder creates a prediction from the previous frame (N-1)

- We can create the prediction from the same postion in the previous frame or from a different position which is offset from the original block position

- For a particular block in the current frame, the block of pixels in the same position in the previous frame is often similar

- However, if objects have moved between frame or if the camera itself is moving, we might find a closer match for the block of picels in a different position in the previous frame

- If we consider the block in the same position to be at location (0,0) then we can specify an offset to different block positions

- This offset is known as a motion vector

- An encoder carries out the following steps when inter-prediciting a square block A in a current frame with reference to a previously coded frame
  1. Encoder selects an offset to a square region B in a previously coded frame. This region in the previously coded frame is the same size as A and is the prediction source
  2. Encoder subtracts each pixel of the prediction source from each pixel of the current block. THe difference is the residual block C
  3. Encoder codes and transmits the residual blokc and the offset motion vector\

- A decoder reconstructs a decoded block using inter predictio with the following steps:
  1. Decoder recieves and decodes the residual block C and the offset
  2. Decoder creates the prediction source B by identifying the same sqaure region in the previously coded frame using an offset recieved from the encoder
  3. Decoder adds each pixel of the residual blokc to each pixel of the prediction source. The result is the decoded block A. This may or may not be identical to the original block A, depending on whether information is discarded during encoding

- The offset from the current block position to the position of a prediction region in a previously coded frame is known as a motion vector

- The process of predicting a blokc using inter prediction can be described as motion-compensated prediction

- The term motion vector can be confusing for at least two reasons. Firstly, when a motion vector points to a prediction block in previous frame, it points to where object have moved from. Secondly, motion vectors point to the best match, which may or may not correspond to actual object motion

- Looking more into the first reason that motion vectors may not point in the direction of motion. If the prediction source is in a previous frame and if objects are moving from frame to frame, then the offset points to where pixels are moving from not where they are moving to

- For the second reason that motion vectors do not necessarily correspond to motion. Understand that when the encoder chooses a motion vector for a block, it is choosing the offset of the best prediction i.e. the prediction that minimizes the number of coded bits for the block, including the coded residual and the coded motion vector. Sometimes this offset corresponds to motion and sometimes it does not. In cases where the section of the image captured withing the block changes from frame to frame, it is difficult to find a match in the previous frame. THe encoder searches fro the best match and finds a match in a seeminly random position. This is not a mistake or a failure - if the offset or motion vector identifies the prediction that minimizes the number of coded bits, then the encoder has done its job successfully, whether or not the motion vector actually corresponds to motion

#### Forward Backward and BiPrediction

- In theory, a video codec can use any data as a prediction source, as long as it has already been coded by the time the encoder makes the prediction. If the data has already been coded

- If the data has already been coded, then it has already been sent to the decoder and so the decoder can create the same prediction

- Possible sources for creating an inter prediction include:
  - The previous frame
  - Older past frames
  - Future frames
  - Combinations of previously coded frames, past and/or future

- Recall that a picture or slice, which itself corresponds to part or all of a picture can be coded as an I, P or B picture or slice using one of the popular video coding standards

- In an I picture or slice all the coding units (CUs) or Macroblocks are coded using intra prediction i.e. there is not option to use inter prediction

- In a P picture or slice, CUs or MBs may be coded using inter prediction with one reference picture or using intra prediction

- In a B picture or slice, CUs or MBs may be coded using inter prediction with two reference pictures which is known as biprediction. They may alternatively be coded using inter prediction using one reference picture or intra prediction

- This means that when encoding a P or B slice, an encoder can choose a mix of prediction types depending on what is best for the current MB or CU. For example, in a B slice, one CU may be efficiently predicted using two prediction sources i.e. biprediction. The next CU may be difficult to predict from previously coded frames and the best predition choice might be to use intra prediction. Thus the difference between and I , B and P slices is in the choices of prediction types that are available

- Instead of predicting from the immediately preceeding frame N - 1, the encoder can choose to predict a block from an older frame, e.g. N-2, N-3

- Predicting from an older frame i.e. a frame that should be displayed before the current video frame is known as forward prediction

- For many blocks, the best prediction may well be found in the previous N-1 frame

- However, in some cases a better prediction might be available in an older frame. For exmaple if there is periodic movement in the scene, we might find a matching block in an older frame rather than in the previous frame

- Alternatively, if the changes from frame to frame are complex and somewhat random, we might simply find a prediction that reduces the residual by looking at an older frame. The frame we choose to predict from is known as a reference frame or reference picture

- The above discussion implies that the more reference frame we consider, the better. However, there are downsides to considering many previous frames as possible reference frames for each block of pixels

- First the encoder has to signal the choice of the prediction frame, which may take more bits than simply assuming prediction from the previous frame. Second, both the encoder and decoder have to store all of the frames that might be used for prediction, which may require more memory to store all of the pixels of the previously coded frames. Third, searching for a prediction match, known as motion estimation is computationally intensive and there is often a diminishing return i.e. point at which it is not worth the computational effort to search a much older reference frame

- Another option is to create an inter prediction from a future frame i.e. a frame that will be displayed after the current frame

- An encoder can predict a block in the current frame N from a region in frame N+1, N+ 2 etc

- This may seems counter intuitive since these frames should be displayed in the future. However, backwards prediction is feasoble if the encoder and deocder can change ther cording order of video frames so that any future frames used for prediction are sent before the current video frame

- Backwards prediction can be useful when areas of a video frame are uncovered

- An inter prediction can also be created by combining pixels in two reference frames

- A biprediction block is formed by averaging each pair of pixels from two source blocks. This biprediction block is then subtracted from the original block to create a prediction residual

- Biprediction can often give a better prediction than uni-directional prediction whihc predicts from a single reference frame. However the encoder needs to send offsets to two prediction source blocks, so biprediction may require more bits to signal the choice of predicition source

- Biprediction has been a feature in video coding since the publication of MPEG1 and MPEG2 video coding standards in the early 1990s. In these early standards, the encoder was restricted to creating a biprediction using a specific past frame and a specific future frame

- Recent standards like H264 and HEVC give the encoder more flexibility so that a bipredicted block can be created from one past and one future frame or from two past frames or from two future frames.

- In theory, more prediction options are possible such as creating a prediction by combining data from three or more frames. Again, biprediction has implications for the way in which reference picture are handled

#### Inter Prediction Block Sizes

- How should the encoder choose the size of the inter prediction block?

- Recall that a video encoder partitions each frame into basic units of coding known as macroblocks or Coding Tree Units.

- These are square blocks, typically a power of 2 to each side e.g. 16x16 pixel macroblocks or CTUs of size 16x16, 32x32 or 64x64

- A prediction block is a subset of a macroblock or CTU

- We could predict the entire macroblock or CTU as one prediction block by choosing a prediction block size equal to macroblock or CTU size. Alternatively, we could choose a smaller block size, such as a square or rectangular block that is msaller than the macroblock or CTU

- Just like in intra-prediction, the best option for inter prediction block size may be tow switch two or more block sizes using larger block for areas of the background wiht less movement and smaller blocks for complex moving regions

- The encoder communicates extra information for every prediction block. As well as signalling the choice of prediction block size and perhaps further prediction mode information, the encoder must also communicate a motion vector for each inter prediction block

- There are a number of ways that the encoder can reduce the amount of extra overhead information, such as by inferring or by predicting some or all of the overhead

- In general, however, smaller prediction block sizes mean more prediction blocks per frame and more information sent to describe the mode and motion vector of each prediction block

- Square prediction blocks are computationally simple to process and require little overhead to signal especially if their dimensions are powers of 2

#### Motion Vectors

- Inter prediction attempts to generate a prediction block or region that is similar to a current block or region. A motion vecotr is an offset from the position of the current block to the position of the prediction block

- A motion vector may or may not correspond to the actual motion of the pixels from one video frame to another

- Eahc motion vector points to the location of the prediction region relative to the current block position. A motion vector has an x-component which indicates the horizontal shift, and a y component, which indicates the vertical shift

- The encoder selects the motion vector that gives the best match to the current block. The best match is the prediction block that minimizes a particular measure of difference e.g. MSE between the current block and the prediction block

- The smaller the difference between the pairs of pixels in the prediction block and the current block, the smaller the calculated value of the error will be

- Inter prediction motion vectors tend to have certain predictable properties, such as:
  - Motion vector magnitudes tend to be clustered around 0 if the camera position is fixed or around a fixed value if the camera is moving
  - Motion vectors in a local area of the image tend to be correlated so the current block motion vector is likely to be similar to neighbouring block motion vectors

#### Sub Pixel Interpolation

- So far motion compensation has been discussed which is inter prediction using motion vectors where each motion vector points to a position in a reference frame that is offset by a number of pixels

- Most times motion vectors cannot be represented with integers thus it would be easier to create a better prediction if we can make it possible to send a non-integer motion vector

- We can do this by resampling the reference frame to a higher resolution, for example, by resampling at half-pixel positions and choosing a motion vector that points to pixels in the re-sampled reference frame

- Interpolated sub-pixel positions are created by combining neighbouring pixel values, typically using filtering. The way in which neighbouring values are combined or filtered has an effect on the quality of the interpolation. Examples of filters include bilinear and bicubic interpolation

- There are two main ways to increase the performance or accuract of sub-pixel motion-compensated prediction
  1. We can use a higher-order interpolation filter. A higher order interpolation filter such as the bicubic interpolation filter can produce a more accurately interpolated reference frame and hopefully a better inter prediction. This comes at a cost of increased computational complexity at both the encoder and decoder since both of them must create the same interpolated reference for prediction

  2. We can increase the sampling density. There is usally no apparent difference between the images produces by the higher density interpolations apart form the larger number of interpolated pixel positions since interpolation doesn't add any new information. However, hgiher-density interpolation makes it possible for motion vectors to point to a greater number of positions between integer pixels. As we increase the resolution of the interpolated frame, our chosen motion vectors can more closely approximate actual interframe motion which of course will take arbitray values

- There are two potential disadvantages of increase interpolation density. First, increased interpolation density requires more computational processing. Both encoder and decoder must generate and store the necessart sub-pixel values, which requires computation and memory. Increasing interpolation density by a factor of two, from quarter to to eight-pixel interpolation, requires four times as many interpolated points to be calculated and stored

- Second, higher precision motion vectors typically require mote bits to encode and transmit

- Regardless of the method of encoding and sending vectors, a motion vector in the range (0,1) will require more bits to encode as the interpolation resolution increases

- At a certain point, the cost of extra bits required to send motion vectors outweighs the benefit of greater motion-compensated prediction accuracy. It turns out that this point depends in part on the design of the interpolation filters. With more sophisticated intepolation filters, a higher interpolation depth can provide an overall compression gain

#### Reference Pictures

- Recall that a block in the current video frame is inter-predicted from a region, typically of the same size, in a previously coded frame known as a reference frame or reference picture

- Both the encoder and deocder need to be able to construct the same prediction for every block which measn that both need to have the same set of reference frames available

- As the encoder processes each block of the current frame, it encodes the block into the coded video bitstream and also deocdes the block to create a reconstructed block which it uses to build up a reference frame

- This mimics the bhaviour of the decoder which also decodes each block to build up a current decoded frame for output and optionally, for use as a reference frame

- In this way, both the encoder and decoder construct identical sets of reference frames

- Low delay configuration is a case where the decoder can always decode and display each picture as soon as it has been recieved

- High delay configuration is a scenario where the decoder has to wait a few frames before displaying decoded frames. This type of configuration can give better compression performance at the expense of an increase in decoding delay

- Coded and reference pictures can be organized in a number of ways, depending on the requirements of the application. These applications include:
  1. To minimize end-to-end delay: In an application such as video calling or video conferencing, it is important that the delay between capturing a frame at the source and displaying it as the destination is as low as possible. A short delay gives a more natural conversational experience
  2. To maximize compression efficiency:For example, biprediction with forward and backward reference frames tends to be more efficient than forward-only prediction, which in turn is more efficient than intra-only prediction. A highly efficient sequence may consist mostly of B-pictures with as few I and P pictures as possible
  3. To provide random access capability: In many applications, it is important that a viewer can start decoding part-way through a sequence with a relatively short delay. This typically requires the use of intra-coded pictures at regular intervals. When a user joins a sequence part-way through, the decoder finds the nearest I-picture and starts decoding from there
  4. To provide scalabily, i.e. the ability to extract a lower-fildelity version of the video clip: For example, pictures that are not used as prediction references themselves can be discarded without affecting the remaining coded pictures
  5. To reduce or limit the storage requirements of the decoder

- Some of these aims may be mutually exclusive. For example, high compression efficiency might be achieved at the expense of signinficant delay and memory requirements at the decoder and vice versa

- In low-delay picture strcutures, the sequence starts with an I-picture, since there are no previosuly coded pictures to predict from. Further I-pictures may be inserted at intervals to enable a decoder to start deocding at a later point and/or re-synchronize if there is a transmission error. If the encoder and deocder are communicating in both directions, for example in a video calling application, then it may not be necessary to insert further I-pictures unless the decoder signals that there has been a transmission problem. eahc of the remaining pictures is coded using P or B prediction i.e. each block is inter-predicted from one or two reference pictures. All blocks are predicted from past pictures - pictures that are older in display order. This means that the decoder can display each frame as soon as it decoded, which minimizes the delay at the decoder. Hence, the contribution of the video codec to end-to-end delay need not be more than a one-frame delay

- In a random-access picture structure, a better compression efficiency can be achieved compared to a low-delay structure assuming an equal number of I pictures at the expense of an increase in decoding delay. The sequence starts with an I picture. For random access capability, it is necessary to insert I pictures typically at regular intervals. The repeating structure of reference pictures is sometimes described as a Group of Pictures. If I-pictures occur once every second, say, then a decoder attempting to start decoding at an arbitrary point has to wait at most one second before it recieves and deocdes a fresh intra-coded picture

- In a hierarchical picture structure, pictures at each layer are predicted using only lower-layer pictures as references. This has two potential benefits:
  1. It is easy to strip out higher layers to create a lower frame rate video clip, for example to reduce the bitrate of the coded video sequence
  2. A hierarchical GOP structure may have better compression efficiency than a non-hierarchical structure

#### Signalling Inter Prediction Choices

- Assuming we have a rectangular block in a current picture that is bipredicted from a past and a future reference picture. In order to decode this blokc, the decoder needs to know the following prediction parameters:
  1. Motion Vector 0: The motion vector (offset) pointing to the first reference block
  2. Motion Vector 1: The motion vector pointing to the second reference block
  3. Reference Index 0: An identifier for the reference picture containing the first reference block
  4. Reference Index 1: An identifier for the reference picture containing the second reference block

- If the current block is predicted from a single reference picture, using P-prediction, the the decoder only needs MV0 and RI0. If it is bipredicted, then it needs all four items listed above

- It is important to communicate these parameters to the decoder as efficiently as possible using the smallest possible number of bits. The prediction parameters for each block can be communicated with the parameters split into base parameters and delta parameters

- The base parameters, suich as motion vector predictor, are either inferred or selected:
  1. Inferred: Base parameters are automatically generated at the decoder, based on previously decoded block parameters. No information is sent in the bitstream
  2. Selected: Base parameters are selected at the decoder froma set or list of parameters generatred from previously decoded blocks. A selection index. identifying the chosen base parameters, is sent in the bitstream

- The delta parameters are either sent or not sent:
  1. Sent: A delta value  i.e. the difference between the base parameters and the actual prediction parameters is encoded and sent in the bitstream. The decoder can add this delta value to the base parameters to create the block prediction parameters
  2. Not sent: No delta value is sent, so the current block prediction parametersare set to be identical to the base parameters

- A decoder can infer the base motion vector automatically based on previously coded information, select it from a list of candidates or generate it by scaling previously coded information

- In H.264, HEVC and VP9, each inter prediction block has one or two motion vectors. Unless the block's inter prediction parameters are inherited, as in HEVC's merge mode, the encoder sends an index signalling the choice of reference picture for each motion vector. In the HEVC case, this is an index into a list of candidate reference pictures, List 0 or List 1

#### Skip Mode

- Skip mode, one of the most common modes in may practical coding scenarios, is a mode where no residual information and no prediction information is sent

- If the inter prediction process results in an accurate prediction, the residual block will contain very little information

- After transform and quantization, the blokcs may contain all-zero data. If the prediction parameters are inferred rather than sent e.g. using HEVC's merge mode, and the quantized residual block are all-zero, then no prediction or residual data needs to be sent

- The decoder simply infers a prediction mode by merging from a neighbouring block, generates a prediction block and this becomes the decoded block data

#### Loop Filter

- The encoder and decoder must use the same prediction source in order to create an identical prediction. This means that both encoder and deocder must form a prediction from decoded rather than original video information

- Video coding is typically a lossy process, which means that the decoded frame is not identical to the original video frame

- The coding process introduces distortion such as blocking and ringing effects

- If the reference frame contains obvious blocking and ringing distortion, the best availbale motion-compensated prediction for the current block is distorted. This means that the residual after prediction will contain siginificant energy, even if the motion-compensated prediction is as accurate as possible

- One solution to this problem is to filter the reference frame to reduce distortion before forming the prediction. If the filtering is successful, the filtered reference frame contains less distortion and it is therefore easier to find an accurate match for the current block

- Both encoder and decoder must carry identical filtering operations. This means that the filter process forms part of the encoding loop and so this type of filtering is often described as a loop filter

#### When Inter Prediction Does Not Find a Good Match

- Inter prediction relies on an assumption that we can find a good match for a block in the current frame by looking at a previously coded frame. For example, if we predict a block in frame N from the previous frame, N-1, inter prediction will work effectively if we can find a block of the same size within a search region, perhaps nearby the location of the block in frame N

- Consider the factors that may make inter prediction work badly. What circumstances might lead to the encoder failing tofind a good predicition for the current block i.e. falling to find a similar block in a reference frame?
  1. Non-translational motion: Video codecs such as H264 and HEVC assume a translational motion model. A block in the current frame is predicted from a block of the same size, shape and orientation in a reference picture, offset by an X/Y motion vector. Of course, objects and features in real-world video scenes do not only move in translational steps. In this scenarios, outside of translation, objects could also rotate, be skewed or scaled and/or any combination of these movements. More complex motion omdels can capture some or all of these types of motions. For example, an affine motion model can represent motion using more parameters rather than the simple two parameters of X/Y translation

  2. Motion smaller than the block size: The choice of block or region size for inter prediction is a compromise. A smaller block size may be capable of more accurately reflecting complex, real-world motion. However, each inter-predicted block requires some overhead to be coded, such as X/Y motion vectors, prediction mode and size of the block itself. As we sae earlier, smaller block sizes can offer more accurate predictions at the expense of greater overhead. Current standards set a lower limit on blokc size, typically around 4 x 4 pixels. Because of the trade-off involved in choosing an inter predicition block size, the codec will often encounter situations where object motion is at a scale smaller than the block size
  3. Illumination changes: Another reason that the encoder may not be able to find an accurate match is changing illumination. Illumination compensation, in which the encoder signals a change in illumination as part of the prediction process, may provide better prediction in these types of scenarios
  4. Random motion, complex motion, fades, etc. : Certain types of motion are notoriously diffcult for block-based video codec to handle efficiently. Motion that appears random, such as water ripples, smoke and explosions, makes it difficult to find a genuine match in a reference picture. Fades and other editing effects such as cross-fade can also be difficult to handle using motion-compensated inter prediction. Techniques such as weighted prediction, a form of biprediction where one referecne may have a greater or lesser weight than the other can be useful for fades

- A video encoder has to encode any clip it encounters, including of course, video scenes containing all of the types of motion and changes mentioned above. If the encoder conforms to one of the present standards such as H264 or HEVC, it is limited to prediction using translational motion. If the encoder cannot find a genuine match for a block using motion compensated inter prediction, it may find a suitable inter prediction from a neighbouring block that just happens to be similar to the current block or it may revert to intra prediction

#### HEVC Inter Prediction

- HEVC achieves efficient inter prediction through a combination of techniques, including:
  - The ability to adapt the PU size from 64 x 64 down to 4 x 4 samples, with varying rectangular block shapes

  - Flexible choices of prediction type, direction and reference

  - Interpolation to sub-pixel positions for accurate motion compensation

  - The ability to merge a number of PUs, sharing one set of prediction parameters across multiple PUs, which makes it possible to efficiently predict motion for irregular-shaped moving regions

  - Adaptive deblocking and smoothing filters to reduce artifacts in the reconstructed picture with the aim of improving further prediction

  - The ability to select between intra- and inter prediciton at a range of block sizes, depending on the video content

  - Candidate list for predicting or copying motion vecotrs from previous blocks, known as merge or AMVP mode

#### Inter Prediction in VVC

### Transform and Quantization

- Recall that we have seen how a video encoder processes a video frame, predicting each block using intra prediction or motion compensated inter prediction.

- The encoder subtracts the prediction from the original blokc to leave a residual block

- The next stage is to process the residual blokc using a block transform and quantization

- After these two processes, the block can be encoded into a compressed bitstream. When the bitstream is decoded, eahc blokc is rescaled and inverse-transformed to create a decoded residual. When the bitstream in decoded, each block is rescaled and inverse-transformed to create a decoded residual

- A block transform has the effect of concentrating the important visual information in a block into a small number of significant values known as transform coefficients

- Quantization is used to remove less siginificant values leaving a small number fo visually significant coefficients to represent the block

- Assuming we have an 8x8 residual block on the left, the pixel information is distributed across the block. After transformation, the coefficient block concentrates most of the information into a few significant coefficients. After quantization, most of the quantized coefficients are set to zero. The quantized coefficient block can typically be coded into a much smaller number of bits than the residual block

- The amount of quantization i.e. the amount of information that is removed can be adjusted to control the trade-off between compression and quality. More quantizatrion gives more compression but reduces image quaility when the blokc is decoded, whereas less quantization gives less compression but increases image quality

- The transform stage converts pixels or smaples into a different representation that is suitable for compression

- Many video codecs use block transforms. A block transform takes a block or pixel or residual sample and converts it into a block of coefficients

- Assuming a block of pixel values on the left each stored as a number that indicates the brightness or luma of the pixel. A transform converts the pixels into a block of coefficients, each of which is a number that indicates the proportion or weight of a frequenct component. Note that in the coefficient block, the coefficients at the top left tend to have much higher magnitudes compared to the coefficients of the lower right. This is one of the useful properties of certain block transforms since it is easier to efficiently encode high-magnitude coefficients when they are goruped together

- A block transform may be reversible which means that applying a forward transform followed by an inverse transform will recreate the original data. By itself, a block transform does not compress the data

- Quantization reduces the information contained in the block of coefficients and makes it easier to compress

- However, it is a non-reversible or lossy process, which measn that the information removed cannot be restored

#### Residual Blocks

- In a video encoder, the output of the prediction process is a residual frame or picture. Each block in the residual picture has been predicted from neighbouring samples in the same frame or from previously coded frames. The better the prediction, the less information remains in the residual picture and so a typical residual picture consists of blocks of small positive and negative samples and lots of zeros

- Residual blocks tend to have characterstics that are challenging for compression. First, the information tends to be spread across the block, rather than concentrated in one place. Second, all of the samples are of roughly equal significance, as they all play an important part in reconstructing the final image block

#### Block Transforms

- A block transform converts residual blocks into transform coefficients blocks that are easier to compress efficiently

- Preferably, the transform will compact the energy or information in a block into a small number of significant coefficients

- After applying a block transform, the transformed block represents the same information, but most of the data in the block are typically concentrated into a small group of large valued coefficients

- The transformed block can be quantized to retain these significant coefficients thus retaining most of the important visual information whilst removing small-valued coefficients that do not contribute much to the image

- A block transform takes advantage of certain features of photographic and video images and certain characteristics of human vision including the follwing:
  1. A typical image or video frame is made up of strong features such as objects, edges and textures, wiht smaller, more subtle variations of texture
  2. Dominant features in images, such as lines and textures, are often important to the overall visual effect
  3. Our vision system responds to these features and we tend to notice them more than we do small , subtle variations in tecture
  4. Dominant features in an image tend to appear as strong spatial frequencies
  5. We can remove weak or small-values spatial frequencies without a siginificant loss of image quality

- A block within an image can be represented as a sum of basis patterns, each of which corresponds to a spatial frequency component in the block.

- Each type of block transform has its own set of basis patterns

- The basis patterns can be thought of as prototypes or building blocks for actual image blocks. Any 4 x 4 image block can be created by combining these 16 basis patterns with different weights by scaling each basis patterns and combining them together

- The set of weights or scales of each basis pattern are the transform coefficient. This means that the forward transform calculates the set of weighting values or coefficients that, when applied to the same set of basis pattern, construct the original image block

- The same process can be applied with different block sizes

- The forward transform takes as its input a block of image or residual samples and outputs the coefficient or weights of each of the basis patterns

- The transform finds the weights for each basis patterns that woudl exactly reproduce the image block

- The inverse transform takes a block of coefficients and calculates the corresponding image block. In other words, the inverse transform synthesizes an image block based on the coefficients or weights of each of the N x N basis patterns

- A block transform should decorrelate and compact information in a block of residual image samples. This means that for a typical image blokc the transform should concentrate the spread-out image information into as few significant or large valued coefficients as possible, which are preferably closely grouped together in the transformed block. Usually this is the top-left of the transform block

- There are multiple types of transforms including:
  1. The Karhunen-Loeve Transform: The optimal transform for a block of samples depends on the actual information in the block. For a given set of input data, we can derive a theoretically optimal transform, according to desirable properties of decorrelation and compaction. The KLT transform can be optimal in certain scenarios. The KLT is a block transform with coefficients derived from a set of input data such as an image or video frame. There are two problems that make the KLT impactical for many image and video applications. First, the KLT is not amenable to fast, computationaly efficient implementation. Real-time implementation would require signinficantly higher computational resources that other alternative transforms. Second, the coefficients of the KLT havbe to be calculated based on an input data set. For a practical video coding application, these coefficients woul dhave to somehow be comminicated from the encoder to the decoder so that the decoder could reverse the transform. If this is not done frequently enough, the KLT coding efficiency will suffer as the transform becomes increasingly sub-optimal for each image block. If this is done frequently, the overhead of communicating the inverse transform to the decoder will reduce the overall compression efficiency. The KLT has not seen widespread practical use
  2. The Discrete Cosine Transform: A popular and widely used block transform is the DCT. Developed in 1973 by Rao and Yip, the DCT has properties that make it attractive for image compression. It approaches the decorrelation and compaction performance of the KLT for typical image blocks though not necessarily for residual blocks. For a particular block size, we need only a single transform design, as the transform does not need to adapt or change depending on the data to be transformed. The DCT of a two-dimensional block of pixels or smaples is seperable, which means it can be carried out using a one-dimensional transform applied twice - once to the rows and once to the columns of the block. The DCT can be implemented in many different ways, including in efficient software and hardware applications
  3. The Hadamard Transform: This has basis patterns constructed from binary values rather than fractional or multi-valued integer functions as with the DCT or Discrete Sine Transform (DST). In these basis patterns, each sample position can have one of only two values, unlike the multi-valued patterns of the DCT. A block transform relies on correlating basis patterns with the features of an image or residual block. If the block contains a range of values, then a multi-valued basis pattern is perhaps more likely to correlate with the content of the block. Hence, a DHT may be suboptimal for typical real-world image blocks containing pixels with a wide range of values. However, a transform such as the DHT with two-valued basis pattenrs may be effectiver in certain cases such as:
      - Small block sizes: WHen the block size is just 2 x 2 samples, a 2 x 2 DCT is identical to a 2 x 2 DGt
      - Certain residual blocks: If the prediction stage has been very effective, the residual block will contain mostly small positive and negative values and zeros. A simple transform such as DHt may be just as effective as a more complex transform at correlating with such small-magnitude, dispersed values
      - Graphic images or flat/simple features: Image blocks withing graphic areas, such as an overlay in a TV image, do not necessarily have the typical range of values of a conventional photographic image. These blocks may correlate well with the simple, two-valued basis patterns of the DHT
  4. Discrete Sine Transform: Unlike the DCT, which is constructed from cosine functions, the DST is based on sinusoidal basis functions. Whilst the DCT can be close to optimal for original image blocks, certain residual blocks may correlate more closely with DST basis patterns

- The DCT can be computed as a matrix multiplication that converts N x N block of samples X into a block of coefficients Y, where X and Y have the same dimensions

- Considering the forward DCT process graphically, the process has the effect of detecting each of the 16 patterns. If the block has a similiar pattern to one of the 16 basis patterns, then the DCT coefficient for that pattern will have a large positive value and vice-versa

- Said differently, the DCT calculates the sign and maginitude of spatial frequencies in the input block

#### Quantization

- Once a block of samples has been transformed into a block of transform coefficients, the coefficients can be quantized

- Quantization reduces the precision of each coefficient, which means that large-valued coefficients lose precision and smalled-valued coefficients are set to zero

- Quantization exploits properties of typical images and of the way we see images

- Adjusting the quantization proces is an effective way of controlliing both compression and image quality

- The gap between possible coefficient values is known as the quantizer step size

- Increasing the step size has two effects. First less information is retained in the quantized values, maing them easier to compress. Second, the rescaled values are increasingly different from the original coefficients, which means that distortion is increased and the decoded image quality will be worse

#### Transform and Quantization in Practice

- The transform and quantization stages in a video codec are closely connected. The transform does not provide compression by itself but it designed to work the with the subsequent quantization stage, which quantizes each transform coefficient

- In a practical codec, the transform and quantizer should be designed with certain goals in mind, including:
  - Maximizing rate-distortion performance - maximum quality and minimum compressed bitrate
  - Minimizing computational complexity
  - Ensuring compatibility between encoders and decoders
  - Providing flexibility, for example, in the selection of transform size and quantizer step size

- In recently developed video coding standards, these goals are satisfied by approaches such as the following:
  - Specify a transform that can be implemented using a minimal number of basic arithmetic operations such as additions, subtractions and binary shifts, with as few mulitplications as possible since these tend to be more computationally expensive than addditions and shifts
  - Specifiy a transform that can be efficiently implemented in different ways to maximize efficiency on different software and hardware platforms
  - Specify a particular approximation to transform weighting factors such as irrational number in the 4 x 4 DCT
  - Avoid divisions and fractional arithmetic if possible
  - Limit the number of bits of precision required during computation. For example, if the input samples are 8 bits, what is the maximum dynamic range required during the computation of the transform and quantization stages?
  - Share aspects of the design across multiple transform sizes where possible
  - Specify the quantizer to give an effective level of control of the the trade-off between quantizer steps size, bitrate and quality

#### HEVC Transform and Quantization

#### Transform and Quantize in H266 Versatile Video Coding

### Entropy Coding

- A video encoder produces many different symbols or syntax elements, containing information such as transform coefficients, prediction choices, block sizes and many other parameters

- Some of the syntax elements occur many thousand of times in even a short clip, while others occur occasionally or just once per video

- Certain syntax elements such as transform coefficients cna have a range of values while others are binary

- The actual value of a syntax element may be statistically related to other syntax element values and other information

- We can take all of these factors into account when we are trying to find an efficient encoding for all the syntax elements in a coded video clip

- An entropy encoder converts a sequence of symbols or syntax elements into a bitstream and an entropy decoder converts the bitstream back into a sequence of symbols

- The entropy encoder and decoder can make use of certain information during encoding and decoding such as:
  - The expectation or proability that the current symbols S has value V, P(S = V)

  - Local statistics or context e.g. what values have already been coded in the current region of the video frame or video sequence

  - The current entropy encoder state

- A video encoder can increase the efficiency of entropy coding by:
  - Preprocessing values before entropy coding
    - Scanning or processing quantized coefficients in a certain order to capitalize on the expected statistical relationship in a block
    - Predicting a parameter value such a motion vector or QP from one or more previously coded values and entropy coding the difference between the actual and predicted values
    - Inheriting a parameter valeu such as a mation compensation mode and vector from previously coded block or region
    - Creating a list of likely values and selecting from the list
    - A combination of some of the above points
  - Estimating the probability of a syntax element having a particular value  e.g. 0 or 1 based on how often it took that value to repeat in the past
  - Estimating the probability of a syntax element having a particular value based on the recent and/or surrounding statistics or context
  - Choosing an entropy coding scheme that matches the number of bits per symbol with the probability of that symbol value occurring

#### Entropy Coding for Video Compression

- The challenge of entropy coding is to efficiently encode every syntax element in a video sequence whilst satisfying several aims as far as possible including:
  - Maximizing compression efficiency by using the smallest number of bits to represent the complete coded sequence
  - Minimizing computational complexity by coding and decoding within the capabilities of practical processors and devices. This might include, for example, ensuring that parallel processors can be used efficiently to handle encoding or decoding
  - Providing an efficient mapping to methods of storage or transmission, e.g. mapping suitable-sized chunks of data to network packets

- Fixed-Length Coding is a type of entropy encoding where each symbol S is mapped to a fixed length codeword, i.e. the number of bits used to represent S does not change. In HEVC's Sequence Parameter Set, symbol sps_seq_parameter_set_id is an identifier parameter that can be in the range 0-15 and is always encoded with a 4-bit binary code. Fixed-length coding does not compress that data. It may suitable for values such as sps_seq_parameter_set_id that only occur infrequently - in this case, once per coded sequence - or values for which the probability of each possible value is the same

- Variable-Length Coding is a type of entropy coding where each symbol S is mapped to a variable-length codeword (VLC), which means that the number of bits used to represent S changes depending on the value of V. For example, an exp-Golob codeword has a variable number of bits depending on the value to be coded. The VLCs can be constructed based on a probability model i.e. based on an estimate of the probability of each value V. This estimate may be fixed, as in the pre-defined tables of earlier standards such as MPEG2 video, or it may change depending on the actual frequency of occurence of each value V. The choice of proability model for encoding S may depend on context i.e. statistics within the local area of the coded sequence

- Arithmetic Coding is a type of entropy coding in which when an arithmetic coder encodes a symbol S, it causes a change to internal variables, namely a range and a position. The position variable is a pointer that indicates a position within the range. As each symbol is coded, the actual value of the symbol V and the probability that the symbol is V cause a change in these internal variables. The position variable is communicated to the decoder as the output bitstream. It is possible for an arithmetic coder to approach the ideal fractional number of bits, which is the information content of each symbol. As with variable-length coding, the proability estimate or proability model may be dynamically updated based on previously coded statistics and the choice of proability model may depend on context

- Binary arithmetic coder is an arithmetic coder that only handles binary input symbols i.e the input symbol can only have values 0 or 1. This means that a non-binary symbol S must be converted to a string of binary values or bins, using a process known as binarization. The binary arithmetic coder workss in a similar way to the arithmetic coder described above. Each bit or bin is coded using a probability model that may be dynamically updated and based on context. In addition, the way in which a non-binary symbol is binarized may also depend on context

- An entropy encoder for video compression should provide efficient compression. At the same time, it is important that the encoder and decoder do not take too much processing power. It is also important to handle practical issues such as synchronization when a when client starts decoding a video clip. A practical entropy coder for video coding, such as the entropy coders specified in standards H264 and H265, tend to involve trade-offs between some or all of the following issues:

  1. Compression Efficiency: Variable-length coders and arithmetic coders make use of a probability P(S=V), i.e. the probability that symbol S has value V. Accuratley estimating P(S=V) can improve compression performance. The probability estimate or probability model can be updated based on previously coded values of S. For example, if the actual coded symbol S is a 1, increase the probability P(S=1) so that the next time S is coded, the estimated probability of 1 is slightly higher. Increasing the number of proability models, such as modelling P(S=V) under different local conditions or contexts, may help to accurately model the probability of each symbol value. However, increasing the number of proability models may make it harder to build up accurate statistics of previously coded values of S, since each condition or context will occur less often. Matching the coded bitrate to the information content of the coded symbols can improve compression performance. This is one of the reason arithmetic coding can potentially outperform variable length coding since arithmetic coding has the capability of outputting a fractional number of bits per input symbol

  2. Computational Complexity: The total number of processing operation may be particularly influenced by frequently occuring syntax elements. If most of the actual syntax elements in a coded video sequence are quantized coefficients, then it is important to minimize the complexity of coding these value. Most modern-day processors have the capability to pipeline and/or parallelize computational processes. In order to exploit this capability, it may be necessary to address certain dependencies in the coding process. For example, if operation B depends on operation A, then B and A cannot be processed in parallel

  3. Synchronization: A decoder must be able to start decoding as certain defined points e.g. at the start of a video sequence or at a key frame or intra-coded frame. It may be advantageous to make certain syntax elements such as higher-level synbtax elements easy to decode quickly. For example, the higher level syntax in the HEVC standard is coded using fixed-length or variable length codes, which makes it relatively easy for a decoder to quickly find a suitabel starting point for decoding. In contrast, HEVC's lower-level syntax is coded using arithmetic coding, which can give better compression but is harder to jump into in the middle of a coded sequence. Both encoder and decoder must use the same proability estimates or proability models, which implies that the probability models must be reset at a synchronization point such as a point at which a decoder starts decoding a video frame. However, resetting the probability estimates too often may reduce compression efficiency

#### Pre-processing

- Video codecs can make use of the relationships between nearby pixels, blocks and frames to compress video data. Entropy coding efficiency can be maximized by organizing certain values produced by a video encoder, before processing them with an entropy encoder. Values such as transform coefficients and prediction parameters may be pre-processed prior to entropy coding for example by:
  - Scanning coefficients in a block to group together non-zero or similar values
  - Differentially prediciting motion vectors before coding the difference
  - Grouping and coding certain features in mulitple passes, such as sign bits

- Pre-processing can help to minimize the information to be encoded, to maximize the efficiency of context-adaptive entropy coding and to improve computational performance, for example, making it easier to pipeline or parallelise entropy coding

#### Probability Models and Context Adaptation

- An entropy encoder can estimate or model the probability that symbol S has a particular value V. For examples if S is binary, a proability model estimates the probability that S is 0 or 1 i.e. P(S=0), P(S=1)

- The actual value of S is 0 or 1. If the actual value is 0, then the probability P(S=0) increases slightly, since we have coded one more value of S=0. If the actual value is 1, the P(S=0) decreases slightly

- We can update the proability model after encoding S, increasing or decreasing P(S=0) depending on whether a 0 or a 1 was encoded. In this way, the proability model adjusts P(S=0) based on the actual encoding statistics. It is an adapative model

- Which model should we choose for encoding S? We could imsply maintain one model for each syntax element. Alternatively, we could mainatain multiple models for ceratin syntax elements and select a model based on the particular syntax element and/or what values have been coded in the local area of the video frame (the context)

- How many proability models should we maintain? There is a trade-off between several factors. If we have more probability models, we can, in theory, track the proability of a particular symbol more accurately. On the other hand, more proability models mean that each individual model adapts more slowly since the actual encoding of a symbol usinf that model occurs less often. Each proability model requires storing and updating variables, so more models may increase storage and computational complexity

#### Variable Length Coding

- A variable length coding scheme maps each symbol value to a binary codeword with variable number of bits

- Preferably, symbol values that are more likely to occur are mapped to shorter codewords, and symbol values that are less common are mapped to longer codewords

- The mapping of a particular symbol value to a particular VLC should be unique and the codeword should be uniquely decodable.

- There are different types of practical VLC schemes including:
  1. Unary Coding: A unary variable length code consists of a string of 1s terminated with a 0, or a string of 0s terminated with a 1. Smaller symbol values are mapped to shorter VLCs, so this coding method may be suitabel for a symbol where smalled vallues are more proabable than larger values. Each codeword can be uniquely coded. Encoding and decoding can be carried out with a simple algorithm. A potential disadvantage of unary VLCs is that the codeword length increases in direct proportion to the value, leading to larger codewords for higher values

  2. Exponential Golomb Coding: Exp-Golomb coding is another coding scheme that is constructed according to a regular pattern. LIke unary coding, smaller symbol values are mapped to shorter VLCs and each codeword is uniquely decodable. Encoding and decoding are slightly more complex than for unary codewords but they can still be carried out algorithmically. An Exp-Golomb VLC can be decoded by reading consecutive 1s until a 0 is detected. The number of ones gives us M. The decoder then reads M further bits and constructs the symbol value. Compared to unary codewords, Exp-Golomb codewords increase in size more gradually, increasing approximately with log2 of the symbol value

  3. Huffman Coding: This is a method of constructing a variable length code table for a symbol based on the probability of occurence of each possible value. Assuming we have seven possible values V of a motion vector component. If we know the probabilities of occurence of each value, we can apply the Huffman algorithm to construct a set of binary VLCs. The most probable value is assigned the shortest codeword, the next most probable value is assinged a longer codeword and so on. A few important points about the resulting VLC include:
      - Each codeword is uniquely decodable. It is not a prefix of any other codeword
      - The size of each codeword increases approximatley with the information content
      - Huffman codewords do not usually exactly match the information content of each value, since Huffman VLCs, in common with other VLCs, are always an integer number of bits
      - Constructing the VLC tabel requires knowledge of the probability of occurence of each value. If the probabilities change, the resulting VLC table changes

  4. Precalculated VLC tables: In practice, the probability of a symbol having a particular value depends very much on the content being coded. In a video frame containing a lot of movement, we might expect the probability of zero vectors i.e. MV = 0, to be lower than in a video frame without much movement. One solution to this problem is to train the entropy coder with expected probabilities, based on a large set of representative video clips and then to specify the codewords in a standard by defining pre-calculated VLCs. This approach was taken in early video coding standards such as MPEG1 video, MPEG2 video and H263. Each VLC table is constructed based on a pre-determined estimate of probabilities

  5. Context Adaptive VLC: Fixed tables of VLCs are not optimal for every video sequence, since the actual probability of each value will vary depending on scene content. ONe solution to this problem is context-adaptive variable length coding (CAVLC) in which the mapping of symbols to VLCs depends at least partly on recent coding statistics

#### Arithmetic Coding

- The variable length coding scheme described above share a disadvantage, namely that VLCs with integral lengths are likely to be sub-optimal since information content can be a fractional number of bits

- The compression efficiency of variable length codes can be particularly poor for symbols with probabilities greater than 0.5, as the best that can be achieved is to represent these symbols with probabilities greater than 0.5 as the best that can be achieved is to represent these symbols with a single-bit code

Arithmetic coding is an alternative to Huffman coding that can more closely approach theoretical maximum compression ratios. An arithmetic encoder converts a sequence of data symbols into a single fractional number and can approach the optimal fractional number of bits required to represent each symbol

#### Binary Arithmetic Coding

- A BAC encoder represents a series of bins i.e. binary values to be encoded, as a binary function that lies somewhere within a range. Each successive bin value makes the Range progressively narrower. The decoder can decode the bin values by identifying the Range pointed to by the binary fractional

- Each bin is associated with a probability model or context model that estimates the probability that the next bin value is a 0 or a 1, P(0) and P(1)

- Coding a bin involves sub-dividing a Range, in proportion to the probability estimates P(0) and P(1)

#### Context Adaptive Binary Arithmetic Coding

#### Entropy Coding in HEVC

#### Entropy Coding in H266 VVC

### Coded Video Filtering

- Video filtering involves applying a digital filter to pixels in a video image to modify or enhance the image in some way. Filtering can be applied for a number of purposes

- Loop filtering is a type of filtering that occurs withing a video encoder and video decoder

- The main purpose of loop filter is to improve the performance of the video codec itself by imporoving the prediction source and therefore improving the performance of prediction

- Reference frames in an encoder can be filtered before creating a prediction for a block to be encoded. The decoder has to create an identical prediction so the same filter is applied to reference frames in the decoder

- Two examples of in-loop filters used in video coding are deblocking and deringing filters. A deblocking filter attempts to reduce distortion at block boundaries. This is the characteristic blockiness introduced by the lossy encoding process that is familiar from over-compressed videos and images. A deringing filter attempts to reduce visible ripples near strong edges in a video image

- In-loop filters affect the visual appearance of the filtered image

- Visual quality is inherently subjective, which means that the extent to which such filters improve the displayed image is a matter of individual opinion. However, if an in-loop filter does an effective job of improving prediction and compression performance, then it also enables coding of higher quality video at a given bitrate

- Lossy compression can provide significant amounts of compression but introduces distortion, sometimes described as quantization noise, into the decoded video image. This distortion often appears in characteristic forms known as encoding artifacts. For example, block-shaped distortions or blocking artifacts have been a characterstic feature of lossy image and video coding since early standards such as H261 and JPEG

- An in-loop filter uses knowledge about the video encoding process to first discriminate coding artifacts from genuine image features and then to correct or reduce these artifacts whilst attempting to retain genuine image features

- For example, blocking artifacts occur next to coding block boundaries and the magnitude of the artifact or the amount by which sample values are distorted is related to the quantizer parameter. A decoder can detect a blocking artifact based on its knowledge of the block boundaries and the current QP. In-loop filters can be considered to be a way of reducing noise such as coding artifacts in the decoded video signal by exploiting knowledge of the characteristics of the noise such as the way in which the video was coded

#### Filtering and Video Coding

- Filtering can be implemented in at least three places in a video codec: as a pre-filter before encoding the video, as an in-loop filter within the encoding and decoding process and/or as a post-filter adter decoding and before display or further processing

- A pre-filter can be used to reduce camera noise or other unwanted variations in the video signal before encoding

- Capturing video in low-light situations can lead to camera noise or graininess in the video image. Such noise may have high-frequency characteristics which in turn would introduce unwanted high-frequency transform coefficients that can increase the bitrate after compression

- Camera shake during video capture can introduce unpredictable motion between frames which may reduce the effectiveness of motion-compensated prediciton and increase the bitrate after compression. A pre-filter that reduces spatial noise such as graininess and/or temporal variation such as camera shake, may result in more efficient video compression. A pre-filter in implemented prior to encoding does not need to be defined in a standard

- A post-filter is any filtering that occurs after decoding and before subsequent processing or display. This could include, for example, filtering to further reduce compression artifacts such as blocking, ringing or maginitude

- An in-loop filter attempts to improve the compression performance of the codec by reducing artifacts in decoded or reconstructed reference frames. Because identical filtering must be carried out in the encoder and decoder,in-loop filters may be defined in video-coding standards. An in-loop filter is designed with the specific aim of improving compression performance

- Essentially, the the job of an in-loop filter is to improve the prediction process by reducing distortion in a reconstructed reference frame

- Some types of distortion are predictable and are a function of the way the video-coding process works. If the codec can identify a distortion or artifact that was introduced by encoding, then it can attempt to filter it to reduce distortion

#### Detecting and Correcting Video Artifacts

- Blocking artifacts are discontinuities across the boundaries between transform and/or prediction blocks in a coded video image

- Blokcing artifacts have a characteristic tiling appearance. The visible edges of a blocking artifact align with the positions of transform blocks and/or prediction blocks when they first appear

- To compensate for such a blocking artifact, we want to adjust the pixel values nearest the boundary to make the progression more continuous

- The aim of a deblocking filter is to identify and reduce block boundary discontinuities that were introduced by the compression process, preferably without affecting features that are in the original image and that happnen to occur next to a block boundary

- Unless the encoder sends extra information to the decoder, the decoder must identify and correct blocking artifacts based on known information about the decoded video image. There are ceratin aspects of blocking artifacts that are helpful here. First blocking artifacts occur next to or neat block boundaries such as transform block or prediction block edges. Thus the effect of a blocking artifact may be strongest in the samples immediately adjacent to the boundary and weaker in samples further away from the boundary. Second, the magnitude of a blocking artifact discontinuity is affected by certain conding parameters such as the quantizer parameter. Hence, a blocking effect may be identified if there is a discontinuity across a block boundary and if the magnitude of the discontinuity is below a certain threshold, which means that it is likely to have been caused by quantization effects and not by an image feature

- Ringing or ripple artifacts are often found adjacent to strong edges in the orginal video image and appear as dark or light ripples that did not exist in the original image. This phenomenom is similar to the Gibbs phenomenom in found in digital filtering

- Higher frequency block transform coefficients tend to have smaller magnitudes and are often quantized to zero. A square wave comprises a sum of increasingly higher frequencies with increasingly smaller magintudes. In a similar way, a strong edge in an image can be represented as a sum of increasingly smaller magnitudes and higher frequency transform coefficients. Removing the higher frequency coefficients by quantizing them to zero means the reconstructed block may exhibit ringing or ripple artifacts

- Ringing artifacts have certain characteristic properties. Each of the distorted segments is a local peak or trough shape. By detecting these distinctive shapes in the reconstructed block, an encoder and a decoder can identify and correct the distortions

- A magnitude offset can be defined as a change in the overall or average magnitude of the samples in a video image block. For example, a block or region of samples may appear lighter or darker than the original samples due to a shift in the magnitude of luma samples. Alternatively, a region may appeart to have shifted colour due to a change in the magnitude of the chroma samples

- Quantization in a video codec can change the magnitude of transform coefficients or set them to zero. When the quantized transform coefficients are inverse transformed, the decoded block may experience a shift in magnitude that manifests as a change in the brightness or in the colotr of the reconstructed image

- Magnitude shifts can also occur due to motion compensation. When the QP is high, the encoder may be forece to choose distorted regions to predict from which can lead to cumulative distortions. The reuslt can be a shift in apparent brightness or a shift in color representation

#### HEVC In-Loop Filtering

#### VVC Filtering

### Storing and Transporting Coded Video

#### Storing and Delivering Coded Video

- Consider a scenario where a video source such as a camera feed is encoded, transmitted across a network, decoded and displayed. Video is captured by the camera at a certain resolution and frame rate. Each video frame is encoded and placed in the encoder output buffer

- Recall that coded video frames often vary in size. For example, an intra-coded frame is usually mich larger than an inter-coded frame due to the greater efficiency of inter-frame prediction. This means that the encoder output bitrate is likely to vary from frame to frame

- Coded frames are transmitterd from the encoder output buffer across a network or a channel. The rate of transmission depends on the network connection or channel capacity and might vary during the communication session

- The encoder output buffer decouples the variable encoded bitrate from the transmission bitrate somewhat but it is common to use bitrate control feedback from the encoder buffer to the encoder to prevent the encoder output buffer from overflowing or underflowing

- At the reciever, video data are recieved from the network at a certain bitrate. Depending on the network, this may be the same as the transmitted bitrate or it might vary depending on the network conditions

- The recieved data are buffered in the decoder input buffer. The decoder retrieves data from this buffer typically at a rate that mirrors the output bitrate from the encoder. Coded frames are decoded and presented for display, preferably at a constant frame rate so that the video appears to the viewer to play smoothly. The decoded frame rate may be the same as or less than the source frame rate

- The encoder might choose to drop frames because it does not have enough computational capacity or as part of a rate control strategy so that the decoded frame rate will be lower than the source frame rate. Frames may also be dropped at the decoder perhaps due to lost or delayed packets or because the decoder is running out of computational capacity

#### Coded Video File Formats

- Recall that when transmitting encoded video, information common to some or all of the frames is stored in parameter sets that may be sent or stored at the start of the sequence in Picture, Sequence and Video Parameter Sets

- Eahc video frame is coded as an access unit (AU), which is a term for a single coded frame. An AU is coded and sent as one or more network abstraction layer units (NALU), each of which is a dat astructure defined in the standard that contains a coded slice, which is all or part of a coded frame

- A decoder can process the coded sequence by receiving the information from start to finish, decoding the set of slices that make up each AU and outputting decoded frames for playback

- A compressed video sequence, suhc as a complete H265 sequence can be stored in a single fiel. For example, the HEVC model (HM) reference encoder, a software implementation of H265 produces a sile containing as encoded sequence and the HM reference decoder processes and decodes this file. The file produced by the HM encoder contains the coded AUs stored sequentially

- Video is typically accompanied by audio, perhaps multiple channels of audio, and other information such as metadata and subtitle tracks. One way of storing all this information in a file is to simple concatenaten the data. Such as a file contains all the information necessary to decode and play a video and audio presentation. However, a simple file structure like this may not be practical for all purposes

- With this structure, a decoder needs to have most or all of the file available beofre it can start playback since the audio is placed after the video at the end of the file. This means that the decoder has to recieve most of the file data before decoding and presenting the video and acccompanying audio. This is not ideal for progressive download or streaming, where it is usually preferrable to start decoding and playback as soon as possible after the file starts to download

- Scenarios such as progressive download, broadcast and streaming may benefit from a more sophisticated file format with interleaving of audio and video data and metadata to make it easier for a client to decode, playback and navigate within the file

- There are different types of file formats including Moving Picture Experts Group 4 (MPEG-4), MPEG-2 transport stream (TS) format and Matroska video format (MKV)

- The ISO base media file format (BMFF) is a standardised format for storing audiovisual data in media files. The popular MP4 file format specified in MPEG4 Part 14 is based on the BMFF. Another document in the same file format standards family specifies how coded H264, H265 or H266 video is mapped to the ISO BMFF/MP$ file structure. Each coded AU becomes one sample in an MP4 file

- The ISO BMFF evolved from the Quicktime format. The MP4 file format is an extension of the ISO BMFF and can optionally use the specification of the advanced video coding/high -efficiency video coding (AVC/HEVC) file format

- A complete movie or video programme can be stored in one or more ISO BMFF or MP4 files. Each of these files contains an audiovisual clip or sequence that is organized as a set of tracks. A file might contain a single video trach with only video only and no audio or a single audio track with audio only and no video. The file could have a simple audiovisual file with one video track and one audio track or it could have multiple video and/or audio tracks e.g. amove with multiple audio channels for surround sounf and different languages

- The ISO BMFF or MP$ file contains a movie or moov metadata part, which describes the tracks and their relationships and a media data or mdat part which consists of a series of coded samples such as coded audio samples or coded video NALU

- Each track contains a sequence of samples. These are units of coded media such as coded video or audio with associated timing information. A player device can use the track information to identify, decode and present samples in the correct time order. To put it another way, the track information tells a player how to play back the video and audio correctly and points to actual coded video and audio

- The ISO BMFF, MP4, AVC and HEVC file format specifications leave some flexibility as to how the metadata and coded samples should be arranged in a file. As we will see, files intended for progressive download or streaming may benefit from being organised in certain ways

#### Transport of Coded Video

#### Video Rate Control

#### Error Handling

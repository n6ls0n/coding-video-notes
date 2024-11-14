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

#### Signalling Intra Prediction Choices

#### Choosing a Prediction

#### HEVC Intra Prediction

#### VVC Intra Prediction

### Inter Prediction

#### Inter Prediction The Basics

#### Forward Backward and BiPrediction

#### Inter Prediction Block Sizes

#### Motion Vectors

#### Sub Pixel Interpolation

#### Reference Pictures

#### Signalling Inter Prediction Choices

#### Skip Mode

#### Loop Filter

#### When Inter Prediction Does Not Find a Good Match

#### HEVC Inter Prediction

#### Inter Prediction in VVC

### Transform and Quantization

#### Residual Blocks

#### Block Transforms

#### Quantization

#### Transform and Quantization in Practice

#### HEVC Transform and Quantization

#### Transform and Quantize in H266 Versatile Video Coding

### Entropy Coding

#### Entropy Coding for Video Compression

#### Pre-processing

#### Probability Models and Context Adaptation

#### Variable Length Coding

#### Arithmetic Coding

#### Binary Arithmetic Coding

#### Context Adaptive Binary Arithmetic Coding

#### Entropy Coding in HEVC

#### Entropy Coding in H266 VVC

### Coded Video Filtering

#### Filtering and Video Coding

#### Detecting and Correcting Video Artifacts

#### HEVC In-Loop Filtering

#### VVC Filtering

### Storing and Transporting Coded Video

#### Storing and Delivering Coded Video

#### Coded Video File Formats

#### Transport of Coded Video

#### Video Rate Control

#### Error Handling

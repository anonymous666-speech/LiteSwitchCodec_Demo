# <center> LiteSwitchCodec: Neural Speech Coding with Causal U-Net in Scalar Latent Space for Real-time Personalized Communications </center>

anonymous authors


## Abstract
Neural speech codecs have significantly progressed in speech communication under low bitrate conditions.
For real-time communication (RTC) applications, these neural codecs need to operate with low computational complexity, minimal latency, and maintain high speech quality at low bitrates. 
Most end-to-end neural speech coding methods use fully convolutional encoders and decoders, with the quantizer implemented as a vector quantizer (VQ), requiring computationally intensive decoders to ensure high-fidelity speech reconstruction.
In this paper, we present LiteSwitchCodec, a lightweight streaming speech codec that uses scalar quantization (SQ), 
reduces the parameters by 38x while achieving competitive quality with the DAC codec and maintaining a balanced parameter distribution between its encoder and decoder.
Moreover, our LiteSwitchCodec can provide personalized services such as voice adaptation (VA) without additional latency.
Traditional voice conversion (VC) model is a pre-processing module before speech coding introducing additional delays, making them unsuitable for RTC scenarios.
Therefore, LiteSwitchCodec incorporates a lightweight causal U-net network to perform VA on the generated token, acquiring fine-grained contextual information in the compression domain.
These transfered tokens are dequantized and decoded to produce the target speaker’s speech.
Leveraging speaker-specific embedding, we focus on developing personalized models that work well for individual target speakers.
Our method enables seamless switching between original voice mode and personalized VA mode with an ultra-low latency of 40 ms.
% To effectively mitigate the quantization noise of VA mode, we design a novel token refinement network to improve speech fidelity.
Extensive experiments and ablation studies demonstrate the effectiveness of LiteSwitchCodec, establishing it as a feasible solution for enhancing VA features.

<!-- 
comments
## Model Overview
<img src="imgs/pipeline.png" alt="Overall Architecture" />
-->
# Demo of original voice mode

"Ref" denotes the reference speech. We have provided samples compressed by various codecs, including both signal processing-based and neural-based methods. In these comparisons, "LiteSwitchCodec@7.2kbps" specifically refers to our original voice model.

##     Demo of female


###    English 

 |Ref |Opus@6kbps| Lyra2@6kbps | EVS@7.2kbps | Opus@8kbps | LiteSwitchCodec@7.2kbps| Lyra2@9.2kbps | EVS@9.6kbps | Opus@10kbps | Opus@16kbps|
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
 |<audio src="demo_orig/Eng/Female/Female_01.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_02.wav" controls preload></audio> |<audio src="demo_orig/Eng/Female/Female_03.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_04.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_05.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_01_liteswtichcodec.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_07.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_08.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_09.wav" controls preload></audio> | <audio src="demo_orig/Eng/Female/Female_10.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |




##     Demo of male


###    English 

 |Ref |Opus@6kbps| Lyra2@6kbps | EVS@7.2kbps | Opus@8kbps | LiteSwitchCodec@7.2kbps| Lyra2@9.2kbps | EVS@9.6kbps | Opus@10kbps | Opus@16kbps|
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
 |<audio src="demo_orig/Eng/Male/Male_01.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_02.wav" controls preload></audio> |<audio src="demo_orig/Eng/Male/Male_03.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_04.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_05.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_01_liteswtichcodec.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_07.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_08.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_09.wav" controls preload></audio> | <audio src="demo_orig/Eng/Male/Male_10.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |





##     Demo of female
###    Mandarin 



|Ref | LiteSwitchCodec@7.2kbps | DAC@8kbps  | Encodec@12kbps   | SpeechTokenizer| 
|:---: | :---: | :---: | :---: | :---: | 
 |<audio src="demo_orig/female/Ref_p501/p501_CN_F1_68.wav" controls preload></audio> | <audio src="demo_orig/female/LiteSwitchCodec/p501_CN_F1_68.wav" controls preload></audio> |<audio src="demo_orig/female/DAC/p501_CN_F1_68.wav" controls preload></audio> | <audio src="demo_orig/female/Encodec/p501_CN_F1_68.wav" controls preload></audio> | <audio src="demo_orig/female/SpeechTokenizer/p501_CN_F1_68.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- |


##      Demo of male
###     Mandarin 

|Ref | LiteSwitchCodec@7.2kbps | DAC@8kbps  | Encodec@12kbps   | SpeechTokenizer| 
|:---: | :---: | :---: | :---: | :---: | 
 |<audio src="demo_orig/male/Ref_p501/p501_CN_M1_70.wav" controls preload></audio> | <audio src="demo_orig/male/LiteSwitchCodec/p501_CN_M1_70.wav" controls preload></audio> |<audio src="demo_orig/male/DAC/p501_CN_M1_70.wav" controls preload></audio> | <audio src="demo_orig/male/Encodec/p501_CN_M1_70.wav" controls preload></audio> | <audio src="demo_orig/male/SpeechTokenizer/p501_CN_M1_70.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- |






# Demo of voice changer mode

## Demo of target timbre 1 from AISHELL3

The “target label” denotes the actual target speech signal. 
“Ref” stands for reference timbre of target speaker.
“source” is the input speech signal. “Original” refers to our original voice mode, while “LiteSwitchCodec” refers to our voice changer mode.

**Please slide the mouse to select different files for listening**.

### English 

 |Target label |Ref | Source | Original | LiteSwitchCodec | DDDM-VC | QuickVC | DiffVC | VQMIVC|
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
 |<audio src="demo_SSB0273_taslp/English/Target label/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/Ref/p361_060_mic2_p361_167_mic2.wav" controls preload></audio> |<audio src="demo_SSB0273_taslp/English/Source/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/Original/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/LiteSwitchCodec/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/DDDM_VC/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/QuickVC/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/DiffVC/p236_503.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/English/VQMIVC/p236_503.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |


### Mandarin 


  
| Target label                                              |  Ref                                                         | Source                                                      | Original                                                    | LiteSwitchCodec                                                | DDDM-VC                                                    | QuickVC                                                     | DiffVC                                                      | VQMIVC|                                                      
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
  | <audio src="demo_SSB0273_taslp/mandarin/Target label/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/Ref/p361_060_mic2_p361_167_mic2.wav" controls preload></audio> |<audio src="demo_SSB0273_taslp/mandarin/Source/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/Original/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/LiteSwitchCodec/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/DDDM_VC/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/QuickVC/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/DiffVC/481_0600.wav" controls preload></audio> | <audio src="demo_SSB0273_taslp/mandarin/VQMIVC/481_0600.wav" controls preload></audio> |
   |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |







## Demo of target timbre 2 from VCTK

The “target label” denotes the actual target speech signal. “Ref” stands for reference timbre of target speaker. “source” is the input speech signal. “Original” refers to our original voice mode, while “LiteSwitchCodec” refers to our voice changer mode.

**Please slide the mouse to select different files for listening**.

### English 

 |Target label |Ref | Source | Original | LiteSwitchCodec | DDDM-VC | QuickVC | DiffVC | VQMIVC|
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
 |<audio src="demo_p231_taslp/English/Target label/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/Ref/p231_008_mic2_p231_076_mic2.wav" controls preload></audio> |<audio src="demo_p231_taslp/English/Source/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/Original/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/LiteSwitchCodec/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/DDDM_VC/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/QuickVC/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/DiffVC/p236_503.wav" controls preload></audio> | <audio src="demo_p231_taslp/English/VQMIVC/p236_503.wav" controls preload></audio> |
 |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |



### Mandarin 

| Target label                                              |  Ref                                                         | Source                                                      | Original                                                    | LiteSwitchCodec                                                | DDDM-VC                                                     | QuickVC                                                     | DiffVC                                                      | VQMIVC|                                                      
 |:--- |:--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
  | <audio src="demo_p231_taslp/mandarin/Target label/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/Ref/p231_008_mic2_p231_076_mic2.wav" controls preload></audio> |<audio src="demo_p231_taslp/mandarin/Source/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/Original/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/LiteSwitchCodec/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/DDDM_VC/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/QuickVC/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/DiffVC/481_0600.wav" controls preload></audio> | <audio src="demo_p231_taslp/mandarin/VQMIVC/481_0600.wav" controls preload></audio> |
   |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- |








 
 
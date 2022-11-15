# video-encoding
video encoding settings and tuning
aomenc's default settings are for best quality, this is like the placebo setting in X265 or preset 1 in SVT_AV1 and tiling is not set so it wil use only 1 tile (the entire frame) with only 1 thread because threading is not enabled by default. I am using libaom-av1 with ffmpeg (both of which I compile myself) with these options:
Code:
-cpu-used 4 -row-mt true -threads 8 -crf 35 -tiles 4x2 -aq-mode 3
-cpu-used 4 : similar to presets in SVT_AV1 higher numbers are faster but increase filesize. 8 is fastest, anything between 3 and 6 will do depending on your systems computing power

-row-mt true : this enables tiling and multithreading

-threads 8 : specifies the number of threads to use in tiling mode I have 4 cores with hyperthreading = 8 threads

-crf 35 : single pass encoding ratefactor, 0 for lossless, higher numbers lower quality. (two pass and three pass are not really worth the hassle)

-tiles 4x2 : sets tiling to 4 rows and 2 columns, significant speedup in encoding for a very small quality loss. Do not use more tiles than available threads

aq-mode 3 : best quality setting for regular video, for other stuff like cartoons or images try 1 or 2 as well.

Experiment with these settings to find optimal quality/filesize/encodingtime for your system

https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/intel-linux/1299412-intel-to-ring-in-2022-with-new-faster-av1-encoder-release/page2

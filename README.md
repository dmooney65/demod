# Disclaimer
This tool is not maintained anymore. I made a better one and it can be cloned from here: https://github.com/cubehub/demod

# Demod

Simple command line application for doing AM or FM demodulation. Uses unix pipes for data transfer. Takes raw IQ data as input and outputs demodulated audio.

From this [blog post](http://andres.svbtle.com/pipe-sdr-iq-data-through-fm-demodulator-for-fsk9600-ax25-reception) can be read why such project/fork exists.

# Install

    git clone https://github.com/andresv/demod.git
    cd demod/src
    mkdir build
    cd build
    cmake ../
    make
    make install

# Use cases
Demodulate and listen audio from FM station IQ data recording

    cat fm_radio_r2.iq | demod -mod WBFM -bandwidth 170000 -maxf 75000 -inrate 230400 -outrate 48000 | play -t raw -r 48k -e signed-integer -b 16 -c 2 -V1 -
    
Notice that fm_radio_r2.iq is recorded using following command

    rtl_fm -f 103.4M -M raw -s 230400 fm_radio_r2.iq

Demodulate FSK9600 raw IQ data recording and pipe output to multimon-ng for packet decoding

    sox -t wav FSK9600raw_rf.wav -esigned-integer -b16 -r 1024000 -t raw - | demod -mod NBFM -maxf 3500 -inputtype i16 -inrate 1024000 -outrate 48000 -channels 1 -squaredoutput | multimon-ng -t raw -a FSK9600 /dev/stdin
    
Notice that here [modified multimon-ng](https://github.com/cubehub/multimon-ng) is used that supports 48000 sps input stream for fsk9600 decoder. Read [here](http://andres.svbtle.com/pipe-sdr-iq-data-through-fm-demodulator-for-fsk9600-ax25-reception) why multimon-ng must be modified instead of converting **demod** output to native 22050 format.

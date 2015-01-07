CPPFLAGS=-std=c++0x -I$(PWD) -g

all:	demod-stdin

demod-stdin:	demod-stdin.cc dsp.cc am_decoder.cc nbfm_decoder.cc wbfm_decoder.cc

.PHONY:	clean
clean:
	rm -f demod-stdin

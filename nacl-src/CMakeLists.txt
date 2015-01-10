cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)

set(CMAKE_CXX_FLAGS "-std=c++11 -stdlib=libc++")
project(demod)

add_executable(demod demod-stdin.cc dsp.cc am_decoder.cc nbfm_decoder.cc wbfm_decoder.cc)

install(TARGETS demod DESTINATION bin)
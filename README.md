# Introduction

Converts text to phonemes.
When using eSpeak phonemes, requires an [espeak-ng](https://github.com/denoming/espeak-ng) fork with `espeak_TextToPhonemesWithTerminator` function. This function allows for Piper to preserve punctuation and detect sentence boundaries.

# Building

## By cmake:

```shell
$ git clone -b master https://github.com/denoming/piper-phonemize.git
$ cmake -B build -G Ninja -D CMAKE_INSTALL_PREFIX=piper-phonemize/staging
$ cmake --build build --parallel
$ cmake --install build
```

## By docker

```shell
docker buildx build . -t piper-phonemize --output 'type=local,dest=dist'
```

Find library and Python wheels in `dist/`

# Using

The `piper_phonemize` program can be used from the command line:
```shell
$ cd piper-phonemize/staging
$ LD_LIBRARY_PATH=$PWD/lib bin/piper_phonemize -l en-us --espeak-data share/espeak-ng-data <<EOF
This is a test.
EOF
{"phoneme_ids":[1,0,41,0,74,0,31,0,3,0,74,0,38,0,3,0,50,0,3,0,32,0,120,0,61,0,31,0,32,0,10,0,2],"phonemes":["ð","ɪ","s"," ","ɪ","z"," ","ɐ"," ","t","ˈ","ɛ","s","t","."],"processed_text":"This is a test.","text":"This is a test."}
```

See `src/test.cpp` for a C++ example using `libpiper_phonemize`.

## Python

The `piper_phonemize` Python package is built using [pybind11](https://pybind11.readthedocs.io).

See `src/python_test.py` for a Python example.

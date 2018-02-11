# deinvert

deinvert is a scrambler-descrambler for voice inversion scrambling. It supports
simple inversion as well as split-band inversion.

## Prerequisites
By default, deinvert requires
[liquid-dsp](https://github.com/jgaeddert/liquid-dsp) and libsndfile.

But it can be compiled without liquid-dsp using the configure
option `--without-liquid`; filtering will be disabled and the result will not
sound as good. It can also be compiled
without libsndfile using the configure option `--without-sndfile`; WAV
support will be disabled, only raw input/output will work.

## Compiling

    ./autogen.sh
    ./configure [--without-liquid] [--without-sndfile]
    make

## Usage

Descrambling a WAV file scrambled with setting 4:

    ./src/deinvert -i input.wav -o output.wav -p 4

Descrambling split-band inversion with a bandwidth of 3500 Hz, split at 1200 Hz:

    ./src/deinvert -i input.wav -o output.wav -f 3500 -s 1200

Note that since scrambling and descrambling are the same operation this
tool also works as a scrambler.

If no arguments are given, deinvert reads raw 16-bit, 44.1 kHz PCM via stdin and
outputs in the same format via stdout. The inversion carrier defaults to 2632
Hz.

    ./src/deinvert [OPTIONS]

    -f, --frequency FREQ   Frequency of the inversion carrier, in Hertz.

    -h, --help             Display this usage help.

    -i, --input-file FILE  Use an audio file as input. All formats
                           supported by libsndfile should work.

    -o, --output-file FILE Write output to a WAV file instead of stdout. An
                           existing file will be overwritten.

    -p, --preset NUM       Scrambler frequency preset (1-8), referring to
                           the set of common carrier frequencies used by
                           e.g. the Selectone ST-20B scrambler.

    -q, --quality NUM      Filter quality, from 0 (worst and fastest) to
                           3 (best and slowest). The default is 2.

    -r, --samplerate RATE  Sampling rate of raw input audio, in Hertz.

    -s, --split-frequency  Split point for split-band inversion, in Hertz.

    -v, --version          Display version string.

## Inversion carrier presets

| No | Frequency |
| -- | --------- |
|  1 | 2632 Hz   |
|  2 | 2718 Hz   |
|  3 | 2868 Hz   |
|  4 | 3023 Hz   |
|  5 | 3196 Hz   |
|  6 | 3339 Hz   |
|  7 | 3495 Hz   |
|  8 | 3729 Hz   |

## Troubleshooting

### Can't find liquid-dsp on macOS

If you've installed liquid-dsp yet `configure` can't find it, it's possible that
XCode command line tools aren't installed. Run this command to fix it:

    xcode-select --install

### Can't find liquid-dsp on Linux

Try running this in the terminal:

    sudo ldconfig

## Licensing

deinvert is released under the MIT license, which means it is copyrighted to Oona
Räisänen OH2EIQ yet you're free to use it provided that the copyright
information is not removed. See [LICENSE](LICENSE).

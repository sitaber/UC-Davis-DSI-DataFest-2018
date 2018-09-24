# ocrd-train

> Training workflow for Tesseract 4 as a Makefile for dependency tracking and
  building the required software from source.

## Install

To build leptonica and tesseract, additional data and install it to a subdirectory `./usr` in the repo:

```sh
  make leptonica tesseract langdata
```

Tesseract will be built from the git repository, which requires CMake,
autotools (including autotools-archive) and some additional libraries for the training tools. See the
[installation notes in the tesseract repository](https://github.com/tesseract-ocr/tesseract/blob/master/INSTALL.GIT.md).

## Provide ground truth

Place ground truth consisting of line images and transcriptions in the folder
`data/train` for training and `data/eval` for evaluation.

Images must be TIFF and have the extension `.tif`.

Transcriptions must be single-line plain text and have the same name as the
line image but with `.tif` replaced by `.gt.txt`.

The repository contains a ZIP archive with sample ground truth, see
[ocrd-testset.zip](./ocrd-testset.zip). Extract it to `./data/train` and run
`make training`.

**NOTE:** If you want to generate line images for transcription from a full
page, see tips in [issue 7](https://github.com/OCR-D/ocrd-train/issues/7) and
in particular [@Shreeshrii's shell
script](https://github.com/OCR-D/ocrd-train/issues/7#issuecomment-419714852).

## Train

```
 make training MODEL_NAME=name-of-the-resulting-model
```

which is basically a shortcut for

```
   make unicharset lists proto-model training
```

Run `make help` to see all the possible targets and variables:

<!-- BEGIN-EVAL -w '```' '```' -- make help -->
```

  Targets

    unicharset       Create unicharset
    lists            Create lists of lstmf filenames for training and eval
    training         Start training
    proto-model      Build the proto model
    leptonica        Build leptonica
    tesseract        Build tesseract
    tesseract-langs  Download tesseract-langs
    langdata         Download langdata
    clean            Clean all generated files

  Variables

    MODEL_NAME         Name of the model to be built. Default: foo
    CONTINUE_FROM      Name of the model to continue from. Default: 
    CORES              No of cores to use for compiling leptonica/tesseract. Default: 4
    LEPTONICA_VERSION  Leptonica version. Default: 1.75.3
    TESSERACT_VERSION  Tesseract commit. Default: fd492062d08a2f55001a639f2015b8524c7e9ad4
    LANGDATA_VERSION   Tesseract langdata version. Default: master
    TESSDATA_REPO      Tesseract model repo to use. Default: _fast
    TRAIN              Train directory. Default: data/train
    NORM_MODE          Normalization Mode - see src/training/language_specific.sh for details. Default: 2
    PSM                Page segmentation mode. Default: 6
    RATIO_TRAIN        Ratio of train / eval training data. Default: 0.90
```

<!-- END-EVAL -->

## License

Software is provided under the terms of the `Apache 2.0` license.

Sample training data provided by [Deutsches Textarchiv](https://deutschestextarchiv.de) is [in the public domain](http://creativecommons.org/publicdomain/mark/1.0/).

# UC Davis DSI DataFest 2018

##### Table of Contents 
* [Introduction](#introduction)
  * [Background](#background)
  * [Team](#team)
* [Why Fine-Tune Tesseract?](#why-fine-tune-tesseract)
* [Using this Demo](#using-this-demo)
  * [Prerequisites](#prerequisites)
  * [Running the Demo](#running-the-demo)
  * [Testing the New Model](#testing-the-new-model)
* [Further Information](#further-information)


## Introduction
#### Background
DSI DataFest 2018 was held September 18-21, 2018 at the [UC Davis Data Science Initiative](http://dsi.ucdavis.edu/). 


**The challenge**: To find/test ways to correctly extract wine and spirit price information from scanned [Sherry Lehmann](https://www.sherry-lehmann.com/about-sherry-lehmann-wine-and-spirits) catalogs and turn the extracted information into usable 
structured data that can be utilized by interested parties such as researchers and wine historians. 

The UC Davis Library has over 200 scanned Sherry Lehmann catalogs spanning multiple years: 1938, 1941, and 1947 to 1988. This 
library collection totals to over 4000 pages, and is part of an ongoing Data Science project at the [UC Davis Libray](https://www.library.ucdavis.edu/).

The layout, fonts and coloring of the catalog pages varies, sometime widely, between catalogs and even within catalogs. 
[Some examples can be see here](https://github.com/sitaber/UC-Davis-DSI-DataFest-2018/wiki/Example-Images).

This introduces an extra layer to the challenge, since a solution that works for a sub-set of pages that are similar 
will not be readily applicable to the whole corpus of catalog images.



#### Team
**ZeroInfinity** 
* Mira Daya: <mmdaya@ucdavis.edu>
* Stanislaw Saganowski: <stanislaw.saganowski@pwr.edu.pl>
* Scott Taber: <sitaber@ucdavis.edu> | <https://github.com/sitaber/UC-Davis-DSI-DataFest-2018>
* Kevin Benelli:  <kbenelli@ucdavis.edu> | <https://github.com/Kevin-Benelli/wine-recognition-ocr>

**Team Approach**:
The team attacked this problem from three angles. 
1. Trying methods of image preprocessing using python
2. Improving character recognition of [Tesseract](https://github.com/tesseract-ocr/tesseract) via fine tuning
3. Parsing the resulting extracted text file to retrieve targeted information

**This Repository**

A self-contained package that demonstrates the teams fine-tuning of Tesseract.

## Why Fine-Tune Tesseract?
A conceptual approach to extracting data from the images is as follows

```
data collection => preprocessing => character recognition => formatting into structured data
```

The data collection was already done for this challenge, so the problem reduces to

```
 preprocessing => character recognition => formatting into structured data
```

Preprocessing can greatly enhance Tesseract’s ability to recognize text from the images, but due to the variety of fonts and layouts of the catalogs, the "out of the box" languages for Tesseract fail to identify some characters and many digits accurately. This inhibits the ability to create structured data and is why fine-tuning was an angle of attack chosen.

### Some Results

To illustrate to effectiveness of training Tesseract to recognize the text in the catalogs, [here are some results of training Tesseract on a small set of training data.](https://github.com/sitaber/UC-Davis-DSI-DataFest-2018/wiki/Results)

![](images/results/Results1.png)

The training was done with a small set of 11 images. The results are promising for such a small training set. The recognition of the digits is improved and the sequences of ``` ...``` also have improved recognition.


## Using this Demo

The fine-tuning was done on a computer running Xubuntu 18.04 LTS, and the procedure outlined is only valid for this operating-system. It can work on others, but is only guaranteed for Xubuntu 18.04 LTS.

#### Prerequisites

1. A computer or virtual machine running Xubuntu 18.04 LTS. An image for this OS can be found at https://xubuntu.org/download

2. The [Tesseract Open Source OCR Engine](https://github.com/tesseract-ocr/tesseract) version 4.0.
This can be installed by running
```
sudo apt install tesseract-ocr
sudo apt install libtesseract-dev
```
For further details please see the [Tesseract wiki](https://github.com/tesseract-ocr/tesseract/wiki)

3. Additional Libraries. 
```
sudo apt-get install libicu-dev
sudo apt-get install libpango1.0-dev
sudo apt-get install libcairo2-dev
```
4. The python library pillow to use `generate_line_box.py`
```
pip install Pillow
```
5. langdata-master from (https://github.com/tesseract-ocr/langdata)

#### Running the Demo

This demo utilizes elements of [ocrd-train](https://github.com/OCR-D/ocrd-train). `Makefile` was modified to suit the needs of fine-tuning Tesseract, and the primary part of ocrd-train used was the python script `generate_line_box.py`, which is called from MakeFile. This python script creates the necessary `.box` files from `.tif` and `.gt.txt` which are located in data/train.


To use this demo, download this repositoy with this link https://github.com/sitaber/UC-Davis-DSI-DataFest-2018/archive/master.zip.


This demo is self contained, and Makefile should be run from the directory in which it is contained. The .tif's and .txt's used as truth are contained in `/ocrd-train-mod/data/train` and are the files used to train Tesseract during DataFest

First, unzip `langadata-master.zip` that was downloaded in part `5.` of Prerequisites to `ocrd-train-mod`

Open Terminal and navigate to the `ocrd-train-mod` directory

Execute the following command
```
make training MODEL_NAME=test CONTINUE_FROM=eng_best
```
NOTE: you may use any name after `MODEL_NAME=` 

The fine-tuning process should now be running. You should eventually see something similar to the image below
![](/images/training.png)

Which mean Tesseract is now being trained.

The number of iterations is set to 300. Simply let the process complete.

To use the newly trained model, it must be copied to the main tessdata folder. For example `/usr/share/tesseract-ocr/4.00/tessdata/`. 

This location may vary depending on your system and how you installed Tesseract. If following this guide, and using Xubuntu installed form scratch, this will be the correct directory.

To copy the new `.traineddata` navigate to `ocrd-train-mod/tessdata/` open Terminal and run
```
sudo cp model_name.trianeddata /usr/share/tesseract-ocr/4.00/tessdata/
```
where `model_name` is the name used when invoking `make`

To generate text with the new trained model run
```
tessearct test.jpg test_out -l model_name
```
Where again, `model_name` is the name used when invoking `make`, `test.jpg` is the image file to run Tesseract on, and `test_out` is the name of the output file (it will be appended with .txt, and any name maybe used i.i not restricted to `test_out`)

#### Testing the New Model

To make comparisons, run Tesseract on one or all of the image located in the `images` folder of the repository using. You should invoke tesseract from the `images` folder, using for example
```
tessearct UCD_Lehmann_0006.jpg 0006_out 
```
This will generate text using the "shipped" Tesseract language eng.traineddata

Then run the following to use the newly fine-tuned/trained language.
```
tessearct UCD_Lehmann_0006.jpg 0006_out_trained -l model_name
```

To compare the generated text files
```
diff 0006_out.txt 0006_out_trained > diff.txt
```
If `> diff.txt` is not used in the above command, the differences will be output to the terminal

The resulting differences may not be overly impressive, but promising enough to warrant further training on the catalog images to improve character recognition.

## Further Information

To learn more about training Tesseract 4.00, see the main Tesseract wiki https://github.com/tesseract-ocr/tesseract/wiki/TrainingTesseract-4.00


Or check out the wiki on this repository **NOTE THIS WIKI IS UNDER CONSTRUCTION**

# UC Davis DSI DataFest 2018

##### Table of Contents 
* [Introduction](#introduction)
  * [Background](#background)
  * [Team](#team)
* [Why Train Tesseract?](#why-train-tesseract)
* [How It Works](#how-it-works)
* [Prerequisites](#prerequisites)

# Introduction
### Background
DSI DataFest 2018 was held September 18-21, 2018 at the [UC Davis Data Science Initiative](http://dsi.ucdavis.edu/). 


**The challenge**: To find/test ways to correctly extract wine and spirit price information from scanned [Sherry Lehmann](https://www.sherry-lehmann.com/about-sherry-lehmann-wine-and-spirits) catalogs and turn the extracted information into usable 
structured data that can be utilized by interested parties such as researchers and wine historians. 

The UC Davis Library has over 200 scanned Sherry Lehmann catalogs spanning multiple years: 1938, 1941, and 1947 to 1988. This 
library collection totals to over 4000 pages, and is part of an ongoing Data Science project at the [UC Davis Libray](https://www.library.ucdavis.edu/).

The layout, fonts and coloring of the catalog pages varies, sometime widely, between catalogs and even within catalogs. 
[Some examples can be see here](https://github.com/sitaber/UC-Davis-DSI-DataFest-2018/wiki/Example-Images).

This introduces an extra layer to the challenge, since a solution that works for a sub-set of pages that are similar 
will not be readily applicable to the whole corpus of catalog images.

The challenge was open-ended, and presented an opportunity for people of all skill levels to gain valuable experience with a data 
science project and to learn about [optical character recognition (OCR)](https://en.wikipedia.org/wiki/Optical_character_recognition). Though the correct extraction of the price information was the primary goal, there were many subtasks that could be tackled to streamline the process and support various steps in the pipeline of data extraction. This included, but was not limited to, creating truth-tables, analyzing the images for patterns, testing and fine tuning OCR engines, and exploring other extraction idea/methods

### Team
**ZeroInfinity** 
* Mira Daya: <mmdaya@ucdavis.edu>
* Stanislaw Saganowski: <stanislaw.saganowski@pwr.edu.pl>
* Scott Taber: <sitaber@ucdavis.edu> | <https://github.com/sitaber/UC-Davis-DSI-DataFest-2018>
* Kevin Benelli:  <kbenelli@ucdavis.edu> | <https://github.com/Kevin-Benelli/wine-recognition-ocr>

**Team Approach**
* Categorize images and running them through [Tesseract](https://en.wikipedia.org/wiki/Tesseract_(software)) to create a benchmark of Tesseract's performance on default settings  
* Train Tesseract with a small sample of fonts from the images and compare to benchmark to see if there is an improvement
* Parsing Tesseract results with regular expression to extract targed information

**This Repository**

Outlines the process of training Tesseract. Includes why this method was chosen, how it was accomplished, the results and issues faced in the attempt to train Tesseract.

# Why Train Tesseract?
A conceptual approach to extracting data from the images is as follows

```
data collection => pre-processing => character recognition => formatting into structured data
```

The data collection was already done for this challenge, so the problem reduces to

```
 pre-processing => character recognition => formatting into structured data
```

Pre-processing can greatly enhace Tesseracts ability to recognize text from the images, but due to the variety of fonts and layouts of the catalogs, the "out of the box" languages for Tesseract fail to identify many alpha characters and digits accuratley. This inhibits the ability to create structed data and is why this approach was chossen.

## Some Results

To illustrate to effectiveness of training Tesseract to recognize the text in the catalogs here are the results of training Tesseract on a small set of training data  






# How it works
# Prerequisites

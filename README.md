# UC Davis DSI DataFest 2018

DSI DataFest 2018 was held September 18-21, 2018 at the [UC Davis Data Science Initiative](http://dsi.ucdavis.edu/). 
**The challenge**: To find/test ways to correctly extract wine and spirit price information from scanned [Sherry Lehmann](https://www.sherry-lehmann.com/about-sherry-lehmann-wine-and-spirits) catalogs and turn the extracted information into usable 
structured data that can be utilized by interested parties such as researchers and wine historians. 

The UC Davis Library has over 200 scanned Sherry Lehmann catalogs spanning multiple years: 1938, 1941, and 1947 to 1988. This 
library collection totals to over 4000 pages, and is part of an ongoing Data Science project at the [UC Davis Libray](https://www.library.ucdavis.edu/).

The layout and fonts of the catalog pages varies, sometime widely, between catalogs and even within catalogs. 
(show some sample pages). 
This introduces an extra layer to the challenge, since a solution that works for a sub-set of pages that are similar 
will not be readily applicable to the whole corpus of catalog images.

The challenge was open-ended, and presented an opportunity for people of all skill levels to gain valuable experience with a data 
science project and to learn about [optical character recognition (OCR)](https://en.wikipedia.org/wiki/Optical_character_recognition). Though the correct extraction of the price information (*and other descriptive information 
such as the name of a wine, its color etc*) was the primary goal, there were many subtasks that could be tackled to streamline the 
process and support various steps in the pipeline of data extraction. This included, but was not limited to, creating truth-tables, 
analyzing the images for patterns, testing and fine tuning OCR engines, and exploring other extraction idea/methods

---
title: Using Tesseract OCR with PDF scans
layout: post
tags: tesseract ocr imagemagick
---

We're at the very beginning of a push to create a centralised repository of company knowledge: a place where new employees **know** they can go to find up to date, definitive information.

Just finding a place to start is a daunting task. Which is how I found myself retrieving a dog-eared photocopy of an introductory document from my folder in my cubby in the office I rarely visit.

I've been keeping this document around "just in case" for about a year and a half now, but I finally have a use for it: it's the perfect lightweight overview from which to spawn a dozen or so wiki pages -- just enough to get our knowledgable staff interested in contributing to and maintaining the information.

We're not sure where the master digital copy of this document got to. It obviously existed a couple of years ago, when the version I photocopied mine from was first printed. Equally obviously, it doesn't exist now.

While fruitlessly searching through our digital archives, the boss had a marvellous idea: if we can't find it, we can get the document scanned and OCR'd instead

**Challenge accepted!** I know how to scan and OCR a document. Our photocopier even has a document feeder. I can probably work this out in the next half hour or so. 

The photocopier emailed me a lovely 13 page PDF, ready to run through `tesseract`.


Wait, no, that doesn't sound right.

    % tesseract file.pdf output
    Tesseract Open Source OCR Engine v3.02.02 with Leptonica
    Error in pixReadStream: Unknown format: no pix returned
    Error in pixRead: pix not read
    Unsupported image type.

**Tesseract doesn't read PDFs.**

I'm sure I used it successfully on a TIFF last time, though. <br>
Imagemagick can probably convert that for me.

    % convert file.pdf file.tiff
    % tesseract file.tiff output
	Tesseract Open Source OCR Engine v3.02.02 with Leptonica
	Error in pixReadFromTiffStream: can't handle bpp > 32
	Error in pixReadStreamTiff: pix not read
	Error in pixReadStream: tiff: no pix returned
	Error in pixRead: pix not read
	Unsupported image type.


Mm, nope. Some slight issues with colour TIFF images there. 

Let's make that an 8 bit TIFF instead.

    % convert file.pdf -depth 8 file.tiff
    % tesseract file.tiff output
    Tesseract Open Source OCR Engine v3.02.02 with Leptonica
    Page 1 of 13
    ...


Okay, now we're getting somewhere. Unfortunately, the result is gibberish:

<blockquote>
sugersm um wmcwankhmsmu n

mm, may k,mvnImq.\-nyv'r1nunr pcv:mclc"s mnsmmsluv uu5|t.eqweu\\me'v
mivvr ucnk‘ lm cenlmsu hcv We r_ mu; M. ZIVEV Var‘ wharwuh
</blockquote>

Why? Well, because the TIFF file is barely readable.

There's one last piece of wisdom here - the [standard resolution](http://www.imagemagick.org/script/command-line-options.php#density) for "convert" is 72dpi. 

If we re-convert that at 300dpi, the result... actually comes out in English. Mostly.

    % convert -density 300 file.pdf -depth 8 file.tiff  
    % tesseract file.tiff output

    
So, **steps to read a PDF document with tesseract**:

1. Convert the PDF document to something else 
2. Make sure that something else is high resolution, and grayscale
3. Use tesseract to read the something else instead


And all of that took about a half hour to work out. 
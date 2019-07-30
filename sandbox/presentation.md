## What is a manuscript, anyway?

* Means "handwritten"
* In a library context it is a contunuoum with two endpoints: 
stuff from (i) handwritten works to (ii) archival records. 
* These things are usually unique. There is one or a few copies that may differ.
* Medieval manuscrpts are handwritten copies, usually manufactured in a special Scriptorium, written by pupils in schools or archival records.

## Worked with one manuscript

I wanted return to [CODICES LATINI HAUNIENSES](http://www.kb.dk/en/nb/materialer/haandskrifter/HA/e-mss/clh.html), both for looking at the data I worked with for more than ten years ago, and hopefully demonstrate that they can still be useful.

I opted for the only book I've actually read, namely Boethius [De Consolatione Philosophiae](https://en.wikipedia.org/wiki/The_Consolation_of_Philosophy). Boethius wrote wrote it AD 523 while awaiting trial and execution. The [manus version of it is on](http://www.kb.dk/permalink/2006/manus/642/eng/) and the [METS](https://github.com/Det-Kongelige-Bibliotek/permalink-manus/blob/iiif_presentation/src/main/webapp/data/manus/642/metsfile.xml)

## Made a quick and dirty image migration 

[Wrote a transform METS to Bash](https://github.com/Det-Kongelige-Bibliotek/permalink-manus/blob/iiif_presentation/sandbox/images/extract_img_info.xsl) creating a shell script that retrieves all the images in a 
manus document, transforms them to tiff and from that to jp2000.

The jp2000 files were installed on IIP Image. Here is folio 6r

JPG http://kb-images.kb.dk/public/Manus/gks1911/gks1911_006x/full/full/0/default.jpg

JSON tech md http://kb-images.kb.dk/public/Manus/gks1911/gks1911_006x/info.json

## A transform from METS to IIIF Presentation API json

* XSLT 3.0 transforms with ease to and from JSON
* My transform is oneway, METS -> IIIF. The use case for the latter is presentation and end user annotation. Not replacing the former METS. 
* [make-iiif.xsl](https://github.com/Det-Kongelige-Bibliotek/permalink-manus/blob/iiif_presentation/sandbox/json/make-iiif.xsl)
* [specimen.json](https://github.com/Det-Kongelige-Bibliotek/permalink-manus/blob/iiif_presentation/sandbox/specimen.json)
* Works, almost. Still unfinished. Lets check with [Mirador](https://projectmirador.org/demo/)
* [Ben Albritton commented](https://twitter.com/bla222/status/1132704573871624193?s=19)

To get a mirador in production requires 

* Completing this transform
* Move this into the running application, such that it be used for all 750+ manuscripts in it.
* Deliver Mirador from JSP in tomcat
* Perhaps style Mirador.

About a week and a half left to get there.

## Experiences and conclusions

* I really like what you can do with IIIF and in particular Mirador
* IMHO, JSON-LD has the basic complications of XML, is not even close provide a comparable technology stack can still not encode text.
* IIIF doesn't really handle chapters and sections. Only headings.
* IMHO, IIIF need a working validator. One that tells you what's wrong with you JSON document. Next Innovation week I might write a IIIF presentation API validator using Schematron.

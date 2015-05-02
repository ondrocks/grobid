# GROBID

[![Build Status](https://travis-ci.org/kermitt2/grobid.svg?branch=master)](https://travis-ci.org/kermitt2/grobid)


## License

GROBID is distributed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0). 

Main author and contact: Patrice Lopez (<patrice.lopez@inria.fr>)

## Purpose

GROBID (or Grobid) means GeneRation Of BIbliographic Data. 

GROBID is a machine learning library for extracting, parsing and re-structuring raw documents such as PDF into structured TEI-encoded documents with a particular focus on technical and scientific publications. First developments started in 2008 as a hobby. In 2011 the tool has been made available in open source. Work on GROBID has been continous as side project since the beginning and is expected to continue until at least 2020 :)

The following functionalities are available:

+ Header extraction and parsing from article in PDF format. The extraction here covers the bibliographical information (e.g. title, abstract, authors, affiliations, keywords, etc.).
+ References extraction and parsing from articles in PDF format. References in footnotes are supported, although still work in progress. They are rare in technical and scientific articles, but frequent for publications in the humanities and social sciences. 
+ Parsing of references in isolation.
+ Extraction of patent and non-patent references in patent publications.
+ Parsing of names, in particular author names in header, and author names in references (two distinct models).
+ Parsing of affiliation and address blocks. 
+ Parsing of dates.
+ Full text extraction from PDF articles, including a model for the the overall document segmentation and a model for the structuring of the text body.

GROBID includes batch processing, a comprehensive RESTful API, a JAVA API, a relatively generic evaluation framework (precision, recall, etc.) and the semi-automatic generation of training data. 

The key aspects of GROBID are the following ones:

+ Written in Java, with JNI call to native CRF libraries. 
+ High performance - on a modern but low profile MacBook Pro: header extraction from 4000 PDF in 10 minutes (or from 3 PDF per second with the RESTful API), parsing of 3000 references in 18 seconds.
+ Robust and fast PDF processing based on Xpdf and dedicated post-processing.
+ Modular and reusable machine learning models. The extractions are based on Linear Chain Conditional Random Fields which is currently the state of the art in bibliographical information extraction and labeling. The specialized CRF models are cascaded to realize a complete document structure.  
+ Full encoding in [__TEI__](http://www.tei-c.org/Guidelines/P5), both for the training corpus and the parsed results.
+ Reinforcement of extracted bibliographical data via online call to Crossref (optional), export in OpenURL, etc. for easier integration into Digital Library environments. 
+ Rich bibliographical processing: fine grained parsing of author names, dates, affiliations, addresses, etc. but also for instance quite reliable automatic attachment of affiliations and emails to authors. 
+ "Automatic Generation" of pre-formatted training data based on new pdf documents, for supporting semi-automatic training data generation. 
+ Support for CJK and Arabic languages based on customized Lucene analyzers provided by WIPO.

The default GROBID extraction and parsing algorithms uses the [Wapiti CRF library](http://wapiti.limsi.fr), but it is also possible to use the [CRF++ library](http://crfpp.googlecode.com/svn/trunk/doc/index.html). These two C++ libraries are transparently integrated as JNI with dynamic call based on the current OS. 

GROBID should run properly "out of the box" on MacOS X, Linux (32 & 64), following the guidelines bellow. GROBID does currently not run on Windows environments because the required and up-to-date CRF native binaries are not yet compiled for this platform (contributors to work on Windows support are very welcome!).

## Installation

See the GROBID Wiki quick start pages: 

+ [GROBID service quick start](https://github.com/kermitt2/grobid/wiki/Grobid-service-quick-start)
+ [GROBID batch quick start](https://github.com/kermitt2/grobid/wiki/Grobid-batch-quick-start)

GROBID build relies on maven, and should be standard with respect to Open Source developments. You normally only need to build the project with maven to have it running. 


## Usage

See the Grobid Wiki pages: 

+ [Grobid service quick start](https://github.com/kermitt2/grobid/wiki/Grobid-service-quick-start)
+ [Grobid batch quick start](https://github.com/kermitt2/grobid/wiki/Grobid-batch-quick-start)
+ [Grobid java library](https://github.com/kermitt2/grobid/wiki/Grobid-java-library)

We recommand to use the Grobid RESTful service for the best performance, in particular for exploiting multithreading. 

The results are provided in XML following a custumization of the TEI, see:

+ [TEI encoding of results](https://github.com/kermitt2/grobid/wiki/TEI-encoding-of-results)

The training and the evaluation of the models are described in the following wiki page:

+ [Training the models of Grobid](https://github.com/kermitt2/grobid/wiki/Training-the-models-of-Grobid)
+ [Evaluation against PubMed Central sample](https://github.com/kermitt2/grobid/wiki/Evaluation-against-a-PubMedCentral-set)


## Credits

The main author is Patrice Lopez (INRIA).

Many thanks to:

* Laurent Romary (INRIA), as project promoter and TEI pope. 
* Florian Zipser (Humboldt University) who developed the first version of the REST API in 2011.
* the contributors from ResearchGate: Vyacheslav Zholudev, Michael Häusler and Kyryl Bilokurov.
* Damien Ridereau (Infotel).
* Bruno Pouliquen (WIPO) for the custom analyzers for Eastern languages.
* Thomas Lavergne, Olivier Cappé and François Yvon for Wapiti.
* Taku Kudo for CRF++
* Hervé Déjean and his colleagues from Xerox Research Centre Europe, for xml2pdf
* and the other contributors (Dmitry Katsubo, Phil Gooch, Romain Loth, Maud Medves, ...)

## References

Please simply refer to the github project:

Grobid (2008-2015) <https://github.com/kermitt2/grobid>

See the [References page](https://github.com/kermitt2/grobid/wiki/References) for more related resources. 

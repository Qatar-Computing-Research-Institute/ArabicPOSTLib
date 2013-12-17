ArabicPOSTLib
=============

ABOUT
--------------------------
Arabic POS Tagger Library is a statistical Tokenizer, Part of Speech and Named Entities Tagger  
that was trained using Conditional Random Fields (CRF++).  
CRF have been used for segmenting/labeling sequential data among other NLP tasks.

CONTENTS
--------------------------
Package content, files, folders

 
How to run the software
------------------------
1 - Command line:


	java -Xmx800m -Djava.library.path=. -jar ArabicPOSTaggerLib.jar <options> < [file to parse]

Parameters:

	ArabicPOSTaggerLib.jar <--help|-h> [--task|-t pos|tok|ner] [--klm|-k kenlmDir] <  filename"
	* options: 
 	*  --help		display help information
 	*  --task		tok:  Parse file using tokenization model
 	*                       pos:  Parse file using both tokenization and pos models
 	*                       ner:  Parse file using tokenization, pos and named entities models   
        *
 	*  --klm		kenlmdir :  Directory with kenlm binary
 	* 

Example:

	java -Xmx2800m -Djava.library.path=./data/ -jar ArabicPOSTaggerLib.jar -t pos < Tweets.txt

For Windows Environment: You may require to explicitly specify the library path:

	java -Xmx1024m -Djava.library.path=./data/ -jar ArabicPOSTaggerLib.jar -t pos -k models <  Tweets1.txt

2- Java API:
    See java documentation for class ArabicPOSTagger.testCase using the following methods: 
    
        public static void processFile(java.lang.String dataDirectory,
               java.lang.String kenlmDirectory,
               java.lang.String inputFile,
               java.lang.String outputFile,
               boolean bDenormalizeText,
               int mode)
           
        public static void processSTDIN(java.lang.String dataDirectory,
                java.lang.String kenlmDirectory,
                int mode,
                boolean bDenormalizeText)
        


How to compile the software
----------------------------
Build the jar:
 
	ant jar
	
Deploy the package to other direcotory:

	ant deploy -Do=<Dest Dir>

Dependencies
---------------
Arabic Text Analyzer used Java Native Interface (JNI) wrapper to access CRF++ functionalilies:
Two files needed from the CRF++ which are:

- CRFPP.jar
- and a platform depandent library
	- 	libCRFPP.jnilib -for Mac OS-
	-	libCRFPP.so -for Linux 86_64-
	-	CRFPP.dll -for Windows-
  
You can download the source code for CRF++ from http://code.google.com/p/crfpp/ 
More details about compiling and building CRF++ is provided below.

- kenlm langauage model
KenLM langauge model binary for querying. This is used used for denormalization using the inpur text as a query; denormalized text is generated. 
The source code could be downloaded from
http://kheafield.com/code/kenlm/

===

To build CRFPP.jar:

	cd <CRF++ MainDir>/java
	make
  
To build libCRFPP.jnilib:

	cd <CRF++ MainDir>/java
	make
	g++ -dynamiclib -Wl,-undefined -Wl,dynamic_lookup -o libCRFPP.jnilib  .libs/libcrfpp.o .libs/lbfgs.o .libs/param.o .libs/encoder.o .libs/feature.o .libs/feature_cache.o .libs/feature_index.o .libs/node.o .libs/path.o .libs/tagger.o  java/CRFPP_wrap.o -lpthread -lm
	
To build libCRFPP.so (Linux):

	cd <CRF++ MainDir>/java
	make
	g++ -fPIC -DPIC -shared -nostdlib /usr/lib/crti.o /usr/lib/gcc/i486-linux-gnu/4.4.3/crtbeginS.o .libs/libcrfpp.o .libs/lbfgs.o .libs/param.o .libs/encoder.o .libs/feature.o .libs/feature_cache.o .libs/feature_index.o .libs/node.o .libs/path.o .libs/tagger.o ./java/CRFPP_wrap.o -lpthread -L/usr/lib/gcc/i486-linux-gnu/4.4.3 -L/usr/lib -L/usr/lib/i486-linux-gnu -lstdc++ -lm -lc -lgcc_s /usr/lib/gcc/i486-linux-gnu/4.4.3/crtendS.o /usr/lib/crtn.o -O3 -mieee-fp -Wl,-soname -Wl,libcrfpp.so.0 -o libCRFPP.so

For Windows environment:

	- Copy the Makefile.lib.msvc to <CRF++ MainDir>
	- access <CRF++ MainDir>
	- run "nmake -f Makefile.lib.msvc"  to build CRFPP.dll
	- access <CRF++ MainDir>/java
	- run "nmake" or "javac org/chasen/crfpp/*.java"
	- jar cfv CRFPP.jar org/chasen/crfpp/*.class

Copy both files to the Arabic Text Analyzer root dir or other destination with the ArabicAnalyzer.jar

CONTACT
--------------------------
If you have any problem, question please contact kdarwish@qf.org.qa or aabdelali@qf.org.qa.

WEB SITE
---------------------------
URL for the project  and the latest news  and downloads
	https://github.com/Qatar-Computing-Research-Institute/ArabicPOSTLib

GITHUB
---------------------------
Where to download the latest version, 
	https://github.com/Qatar-Computing-Research-Institute/ArabicPOSTLib


LICENSE
------------
This code is licensed under the LGPL except the binaries and libraries in the depadencies which 
have their own licenses, listed below.  See the references in these files for more details.  
 - CRF++
 - KenLM

For the rest:

    Arabic POS Tagger Library is a free software: you can redistribute it and/or modify
    it under the terms of the GNU Lesser General Public License as published
    by the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    Arabic POS Tagger Library is being made public for researhc purpose only. 
    For non-research use, please contact:
        Kareem M. Darwish <kdarwish@qf.org.qa>
        Ahmed Abdelali <aabdelali@qf.org.qa>
    
    This library is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU Lesser General Public License for more details.

    You access a copy of the GNU Lesser General Public License
    at <http://www.gnu.org/licenses/>.


COPYRIGHT
----------------------------
Copyright 2013 QCRI

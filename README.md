# parallel-loader
Bash script to split and load big size xml files into Oracle

## Preamble
Most of the time, big size XML files lock allocate a lot of resources and they are pretty slow for a single operation of bulk load and this is rather dangerous and may be pretty complex to handle BUT this process can be parallelized and may be indeed faster.
Bash allows this as far as processes are safely separated.

## XML files structure
Big size XML files share almost the same design as they start first with a line reporting XML version simply like:
<?xml version="1.0"?>
But they may also report encoding and other interesting aspects like namespaces and DTD (document type definitions) but for the purpose of this script we do not get into details but there may be just a few.
Next we find the container of all records and the closure of this tag appears and the end of the file as last line.
For more details you may visit:
http://books.xmlschemata.org/relaxng/relax-CHP-11-SECT-1.html
https://en.wikipedia.org/wiki/Document_type_definition

## BASH code
Code is organized into functions in order to easy up the procedure and follows a 'Divide et impera' approach that culminates with an XML loader process of each portion taken from the original file.
For details about functions within BASH, you may visit:
https://linuxize.com/post/bash-functions/

## Track of the process
The script checks the existance of an XML file within a folder and checks if it is in read/write status (it is not still under upload process) and then it counts the amount of lines of the contents; if it is below the limit set at the beginning of the file it goes ahead with loading it otherwise it takes off the first 2 lines of code and it stores them into a file called 'header.txt' and it repeats the same procedure for the last line and it stores it into a file called 'footer.txt'. Next it stores the amount of lines of the earlier limit into a first file and then it removes them for the body text and it creates the first file called 1.xml as result of the junction of header.txt + first amount of xml code + footer.txt and it starts loading it using sql loader. The same operation is performed with the amount of the remaining XML code till the end of lines.

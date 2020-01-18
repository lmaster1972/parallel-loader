# parallel-loader
Bash script to split and load big size xml files into Oracle

## Preamble
Most of the time, big size XML files lock allocate a lot of resources and they are pretty slow for a single operation of bulk load and this is rather dangerous and may be pretty complex to handle BUT this process can be parallelized and may be indeed faster.
Bash allows this as far as processes are safely separated.

## XML files structure
Big size XML files share almost the same design as they start first with a line reporting XML version simply like:
<?xml version="1.0"?>
But they may also report encoding and other interesting aspects like namespaces and DTD (document type definitions) but for the purpose of this script we do not get into details but there may be just a few.
Next we find the container of all records

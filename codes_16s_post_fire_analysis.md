### This file contains the code that I used to analyze the 16S post-fire microbiome data. We will go from raw data to the files which we want to import in R
### Qiime2
### First of all we have to import the data in Qiime2, in order to do that we have to create a .csv file which contains columns such as sample-id, absolute-path, direction (forward or reverse)
echo 'sample-id,absolute-filepath,direction' > manifest.csv
for i in *R1* ; do echo "${i/_R1.fastq},$PWD/$i,forward" >> manifest.csv
for i in *R2* ; do echo "${i/_R2.fastq},$PWD/$i,reverse" >> manifest.csv

### Use the import command to convert all of your paired end sequences to a qiime artifact
qiime tools import --type 'SampleData[PairedEndSequencesWithQuality]' --input-path manifest.csv --output-path demux_16s_post.qza --input-format PairedEndFastqManifestPhred33

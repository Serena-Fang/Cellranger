# Cellranger

## Download Cellranger
Firstly, we need to download Cellranger from the website: https://www.10xgenomics.com/support/software/cell-ranger/latest/tutorials/cr-tutorial-in. 

Then, add it to your $PATH
```export PATH=/n/data1/hms/dbmi/park/serena/yard/apps/cellranger-7.1.0:$PATH```.

## (Optional) Bamtofastq
Cellranger takes in FASTQ files. If start with BAM files, we need to use ```bamtofastq``` to convert BAM files to FASTQ files. 
```bamtofastq --nthreads=8 /path/to/mydata.bam /path/to/home/directory```

More information about ```bamtofastq``` on this website: https://www.10xgenomics.com/support/software/cell-ranger/latest/miscellaneous/cr-bamtofastq

## Cellranger Count
Then I ran ```cellranger count``` to process my gene data (to obtain barcodes):
```
cellranger count --id=BRCA5 \
                  --transcriptome=yard/run_cellranger_count/refdata-gex-GRCh38-2020-A \
                  --fastqs=output/brca5/Count_CA098_BRCA_0_1_HNV7MDSXY \
                  --sample=bamtofastq \
                  --localcores=8 \
                  --localmem=32
```
This code is extracted from my experiment. You need to change the arguments for your own gene files.
You can view this website https://www.10xgenomics.com/support/software/cell-ranger/latest/analysis/running-pipelines/cr-gex-count for more details of the arguments.

## Output files
A successful cellranger count run should conclude with a message similar to this:
```
Outputs:
- Run summary HTML:                         /opt/sample345/outs/web_summary.html
- Run summary CSV:                          /opt/sample345/outs/metrics_summary.csv
- BAM:                                      /opt/sample345/outs/possorted_genome_bam.bam
- BAM index:                                /opt/sample345/outs/possorted_genome_bam.bam.bai
- Filtered feature-barcode matrices MEX:    /opt/sample345/outs/filtered_feature_bc_matrix
- Filtered feature-barcode matrices HDF5:   /opt/sample345/outs/filtered_feature_bc_matrix.h5
- Unfiltered feature-barcode matrices MEX:  /opt/sample345/outs/raw_feature_bc_matrix
- Unfiltered feature-barcode matrices HDF5: /opt/sample345/outs/raw_feature_bc_matrix.h5
- Secondary analysis output CSV:            /opt/sample345/outs/analysis
- Per-molecule read information:            /opt/sample345/outs/molecule_info.h5
- CRISPR-specific analysis:                 null
- Loupe Browser file:                       /opt/sample345/outs/cloupe.cloupe
- Feature Reference:                        null
- Target Panel File:                        null
Waiting 6 seconds for UI to do final refresh.
Pipestance completed successfully!
yyyy-mm-dd hh:mm:ss Shutting down.
Saving pipestance info to "tiny/tiny.mri.tgz"
```
This code is extracted from website, not from my experiment. I used the web_summary to check for gene data quality. I used barcode matrices for further processing.


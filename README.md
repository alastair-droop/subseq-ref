# subseq-ref

The `subseq-ref` tool extracts a subsequence from a FASTA and GTF file pair, returning the subset and the overlapping GTF features. The returned GTF feature coordinates are updated to match the returned FASTA file.
 
## Usage

~~~bash
subseq-ref [-h] [-v] [-V {error,warning,info}] [-p <n>] [-n <n>] [-u]
           [-l <name>] [-e] [-o <stem>]
           <region> <GTF> <fasta>
~~~

~~~
Extract a subsequence from a FATSA and GTF file pair

positional arguments:
  <region>              region to extract (chr:start-end), 1-based
  <GTF>                 GTF file
  <fasta>               FASTA file

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -V {error,warning,info}, --verbose {error,warning,info}
                        Set logging level
  -p <n>, --padding <n>
                        padding length
  -n <n>, --line-length <n>
                        output FASTA line length
  -u, --update-region   update specified region based upon GTF feature
                        overlaps
  -l <name>, --chr-label <name>
                        output chromosome name
  -e, --extended-header
                        provide extra FASTA header information
  -o <stem>, --output-stem <stem>
                        output file stem
~~~

## Notes:

* Region matching is performed first on the chromosome ID. The FASTA header is taken as the FASTA header line before any whitespace characters.
* When `-u` is specified, the selected region is updated to enclose all GTF features that overlap the input region.
* When padding is specified (`-p` is not zero), the FASTA and GTF files will be padded. with `<n>` nucleotides symmetrically.
* By default, the returned FASTA & GTF chromosome name is the same as the input chromosome. This can be changed with the `-l` argument.
* The output file pair is named by the value given in the `-l` argument, or (by default) by the input chromosome.
* If `-e` if specified, extra information is written into the FASTA header.

## Example:

To extract the CD99 gene from chromsome X (it is in the PAR region, and thus also occurs on chromosome Y), returning a new mini-chromosome called `CD99` from GRCh38 GTF and FASTA files:

~~~bash
subseq-ref -lCD99 chrX2691179-2741309 GRCh38.gtf GRCh38.fasta
~~~

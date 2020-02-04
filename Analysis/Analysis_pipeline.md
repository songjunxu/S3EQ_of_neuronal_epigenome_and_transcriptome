# General Analysis

## Data Resource
GSE117462

## FASTQC of raw reads, generate summary

## ChIP-seq analysis
1. Sequences were aligned using Bowtie v2.1.0, allowing for ≤2 mismatches to the reference in 50bp.
2. Uniquely aligned reads were confirmed for H3K36me3 ChIP-sequencing and used for subsequent analysis.
3. Peak calling was performed using SICER (Xu et al. 2014), whereas DiffBind (Ross-Innes et al. 2012) was used to identify the differential histone modification sites between the two different methods.
4. Integrated profiles were created by averaging the observed signal for each bin for the selected set of relevant genes using deepTools computeMatrix (-a 5000 –b 5000); values displayed indicate fragments per 50-bp bin per million mapped reads.
```unix
plotFingerprint -b *.bam  minMappingQuality 30 --skipZeros --numberOfSamples 50000 -T "Fingerprints of new samples" --plotFile new_fingerprints.png --outRawCounts new_fingerprints.tab

computeMatrix scale-regions -b 5000 -a 5000 -R --skipZeros -o
```
5. Enrichment of islands over genome was assessed using HOMER software. By default, HOMER used the DESeq2 rlog transform to create normalized log2 read counts, thereafter generating log2 transformed enrichment relative to a specific genomic category (Heinz et al. 2010).
6. Gene Ontology was analyzed using the Database for Annotation, Visualization and Integrated Discovery (DAVID) Bioinformatics Resource specifying for biological processes. 
7. IGV was used to visualize sequencing coverage

## RNA-seq analysis
1. Sequences were aligned using STAR-2.5.2a(Dobin et al. 2013).
2. Raw gene read counts with default parameters were used to compute fold changes and significance of expression differences using DESeq (Simon 2010). The log expression values for each gene were averaged over each treatment group, and the log2 fold change was computed.
3. Heat maps of raw reads were generated using R’s pheatmap function with default parameters.
4. Unsupervised clustering was performed by pheatmap in default settings.
```unix
multiBigwigSummary bins -b *.bw -out .npz --outRawCounts scores_per_transcript.tab
```
5. Alternative splicing was quantified using the percent spliced in (PSI) metric using Multivariate Analysis of Transcript Splicing (rMATS, v3.2.4). For each event, rMATS reports counts supporting the inclusion (I) or splicing (S) of an event. To reduce spurious events due to low counts, we required all of the samples to have I ≥ 10 and S ≥ 10. For these events, the PSI is calculated as PSI = I/(I + S).

6. IGV was used to visualize sequencing coverage.
toTDF .wig .tdf mm9

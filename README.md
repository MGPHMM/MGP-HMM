# MGP-HMM
MGP-HMM: detecting genome-wide CNVs using an HMM for modeling mate pair insertion sizes and read counts
by Seyed Amir Malekpour, Hamid Pezeshk and Mehdi Sadeghi


Input to the MGP-HMM is a Mapview file - alignment from MAQ (http://maq.sourceforge.net/) by Li, H., J. Ruan, and R. Durbin, Genome Res, 2008. 18(11): p. 1851-8.

The order of running programs is as follows:
1-	MatePairStat.m  
Takes the MAQ alignment file (http://maq.sourceforge.net/) and derives the required information from this file. These information are analyzed in the next steps for detecting genome-wide copy number variation. 

In the first line of this program indicate the path to the MAQ file. The default path is "D:\out.aln.txt".

2-	SegmentationAlgorithm.m   
Assigns each mate pair to the relevant genomic segment.

In this program, you can initialize the genomic segment size (in base pair), genome size, and length of each read in a mate pair. 

Default values of these parameters are segment size=150; genome size =5,000,000; read length=36.

3-	MAIN.m   
This is the main program which detects genome-wide deletions and tandem duplications. 

In this program, you are required to specify the number of genomic segments (T), mean insertion size in the clone library, average number of reads that are mapped to each genomic segment (lambda), and number of EM iterations. Default values for these parameters are T=30,000; Insertion Size=170; lambda=45, iteration=10.

Indeed, having 30,000 genomic segments of length 150 bp (as specified in step 2) means that CNV detection will be done in the first 4.5 million bp of the chromosome.
                      

After running above programs, predicted state of genomic segments are saved in a variable that is called final_path, with numbers in the range of 1 to 11 which correspond to the following states:


state	
1	Diploid state
2	Genomic segment with 3 non-tandem copies
3	Genomic segment with 4 non-tandem copies
4	Genomic segment with 5 non-tandem copies
5	Genomic segment with 6 or higher non-tandem copies
6	heterozygous deletion
7	homozygous deletion
8	Genomic segment with 3 tandem copies
9	Genomic segment with 4 tandem copies
10	Genomic segment with 5 tandem copies
11	Genomic segment with 6 or higher tandem copies






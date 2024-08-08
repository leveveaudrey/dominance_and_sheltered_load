please cite 	Le Veve, A, Genete, M., Lepers-Blassiau, C., Ponitzki, C., Poux, C., Vekemans, X., Durand, E., Castric, V., 2024. The genetic architecture of the load linked to dominant and recessive self-incompatibility alleles in Arabidopsis halleri and A. lyrata. eLife 13. https://doi.org/10.7554/eLife.94972.2

Le Veve, A., Burghgraeve, N., Genete, M., Lepers-Blassiau, C., Takou, M., De Meaux, J., Mable, B.K., Durand, E., Vekemans, X., Castric, V., 2023. Long-Term Balancing Selection and the Genetic Load Linked to the Self-Incompatibility Locus in Arabidopsis halleri and A. lyrata. Mol Biol Evol 40, msad120. https://doi.org/10.1093/molbev/msad120 


I) generate the VCF files
	
	The VCF file were generated with pipeline "sequencing_genome_vcf.py" than take a reference genome (-r) , a file than contained genomic data files name (-i) and a bed file (-b)
		ex: sequencing_genome_vcf.py -d -o nivelle_halleri -r Arabidopsis_lyrata.v.1.0.23.dna.genome.fa -i nivelle -b lyrata_control.bed -p 2

II) Generate file with annotation of each position in a reference genome 

	To determined the 0 fold, 2 fold and 4 fold degenerates sites in the reference genome, we used a published pipeline corrected (bug in original version) than take a gff and a fasta file of the reference genome 
	and we generate a big csv file with the annotation predicted for each position (ex:python NewAnnotateRef2.py Arabidopsis_lyrata.v.1.0.23.dna.genome.fa Arabidopsis_lyrata.v.1.0.23.gff3 -o > lyrata.csv )


III) Determine the position fixed

	To list all position fixed and different of the reference genom in your dataset, you must used the python code "1_fix_pos_vcf.py". Because this code was write for a particular researches, you must
	change the first lines to define your region study, with the name of the chromosome on line 1, the first position of your first region on line 2, the last position of your first region on line 3,
	the first position of your second region on line 4, the last position of your second region on line 5. Moreover, you must change the name of your VCF file on line 12 and coordonate of the 	
	first line of your VCF on line  21.
	you obtain a csv file with the chromosome and the position of all fixed positions.

IV) Analyse of sheltered load by individual 

	To analyse the sheltered genetic load in each individual in your dataset, you must used the python code "2_analyse_vcf_individu.py". Because this code was write for a particular researches, 
	you must change the first lines to define your region study, with the name of the chromosome on line 6, the first position of your first region on line 7, the last position of your first region 
	on line 8, the first position of your second region on line 9, the last position of your second region on line 10. Moreover, you must change the name of your VCF file on line 13 and coordonate 
	if the first line of your VCF on line 18.
	you obtain a csv file with the name of the individual, the number of mutations on 0 fold degenerate sites and on 4 fold degenerate sites, the number of total mutations and the ratio of 
	mutations on 0 fold degenerate sites and on 4 fold degenerate sites. The mean level of dominance at the S locus was add manually. 

V) Analyse of sheltered load by reconstituted haplotype

	To analyse the sheltered genetic load in each haplotype reconstituted in your dataset, you must previously build a csv file with the chromosome, the position, the reference nucleotide, and 
	the annotation of the position found in "genom_analysis.csv". In this file, each individual correspond at the first and second parents follow by the corresponding descendant. For more details,
	see the exampl "phase_input_file.csv".
	Moreover, you must generate a fasta file with the reference genome for your region studied ("Slocus_7.fasta" for an exempl).
	Then, used the python code "3_phase_S_allele.py". Because this code was write for a particular researches, you must change the line 360 to name your population study.
	Moreover, you must defined your first region studied by the name of the chromosome on line 444, the first position of your region on line 445, the last position of your region on line 446.
	You must also define your second region studied by the name of the chromosome on line 510, the first position of your second region on line 512, the last position  on line 513. 
	You obtain a csv file with the genotype in each position on your chromosome for each haplotype reconstituted ("S_allele_phase_output.csv"). You obtained also a csv file with the name of the 
	haplotype, the S allele associated and the population of the haplotype, the number of mutations on 0 fold degenerate sites and on 4 fold degenerate sites on haplotype, the number of total 
	mutations,the ratio of mutations on 0 fold degenerate sites and on 4 fold degenerate sites, the number of false position (genotype of offspring different of two parents) and the number of
	position not possible to determine. The level of dominance of S allele was add manually ("vcf_analysis_haplo_del.csv"). The third CSV files presents, for each S allele represented by more of 2
	copies, the S allele and the population of the copies, the number of copies presented,the number of fixed mutations on 0 fold degenerate sites, the number of total fixed mutations and the 
	number of total mutations considered. The level of dominance of S allele was add manually ("vcf_analysis_allele_fixe.csv"). The last files generate are fasta files with the different haplotypes
	reconstituted for the two regions independently ("haplo_reconstruction_ARK3capture.fa" and "haplo_reconstruction_uboxcapture.fa") and the two regions together 
	("haplo_reconstruction_FUSIONcapture.fa").

For test the pipeline, please, download and unzip all zip files with code. the "post_analysis" file contain the R script used on the paper 

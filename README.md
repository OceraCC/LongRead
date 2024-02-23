Long Read Genome Assmbly Exercise
##Firstly download the filtered SRR13577846 fastq file, then do fastqc for quality check
 fastqc SRR13577846.fastq

##install hifiasm, then run the assembly
git clone https://github.com/chhylp123/hifiasm
cd hifiasm && make
./hifiasm/hifiasm -o SRR13577846.asm -t 32 SRR13577846.fastq

##convert gfa to fasta format
awk '/^S/{print ">"$2"\n"$3}' SRR13577846.asm.bp.p_ctg.gfa > ../fasta/p_ctg.fasta

##Quast quality check
/home/inf-54-2023/bin/quast-5.2.0/quast.py fasta/p_ctg.fasta

##BUSCO quality check
busco -i p_utg.fasta -m genome --auto-lineage-euk
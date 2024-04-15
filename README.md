# Counting
FunctionalGenomics_Project

#htseq_default

# Load necessary modules
source /apps/profiles/modules_asax.sh.dyn
module load htseq

MyID=aubclsc0328
CountHT=/scratch/$MyID/FinalProject/Counts_HTSeq
MAPD=/scratch/$MyID/FinalProject/Map_Hisat2
REFD=/scratch/$MyID/FinalProject/ReferenceGenome
RESULTSD=/home/$MyID/FinalProject/Counts_H_S_2024      

cd $FinalProject
mkdir Counts_HTSeq
cd $FinalProject
cd $CountHT

git clone https://github.com/htseq/htseq
cp $CountHT/htseq/HTSeq/scripts/count.py .

# List of variables
variables=("SRR13308380" "SRR13308381" "SRR13308382")

# Iterate over each variable
for var in "${variables[@]}"
do
    # Create directory
    mkdir "$var"
    
    # Run HTSeq count
python -m HTSeq.scripts.count -f bam -o $CountHT/"$var"/"$var".gtf $MAPD/"$var"_sorted.bam $REFD/Paralichthys_olivaceus.gtf > $CountHT/"$var"/"$var".tab
done


#If received error try running script in the folder where you have bam file and make sure count.py is in same folder.


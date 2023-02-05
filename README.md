# Synteny_traning
Learning record for comparative genome analysis<br>
<br>
<b>1. Genome preparation :</b> <br>
PLAZA database download ".pep" ".gff" files (CDS sequence and chromosome information)<br>
Shorten species name as three letters. Unify species name in GFF file.<br>
<b>Note: In paper, it only kept the species name, gene name, chromosome start position and end position information. However, kept the GO and KEGG annotation in GFF file will contribute to the synteny analysis of specific gene family. </b><br>
<br>
<b>2. Install Diamond and MCScanX on linux system:</b> <br>
Diamond: sequence aligner for protein and translated DNA searches (https://github.com/bbuchfink/diamond)<br>
MCScanX: view multiple alignment of syntenic blocks and downstream analysis tools (https://github.com/wyp1125/MCScanx)<br>
Cloud computer: ubuntu<br>
Download Diamond:<br>
wget http://github.com/bbuchfink/diamond/releases/download/v2.0.14/diamond-linux64.tar.gz<br>
tar xzf diamond-linux64.tar.gz<br>

Error:

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

<b><1> Download Diamond:<br></b>
```Bash
wget http://github.com/bbuchfink/diamond/releases/download/v2.0.14/diamond-linux64.tar.gz
tar xzf diamond-linux64.tar.gz
```
(wget: linux 内置软件指令）

```Bash
root@lyt:~/lyt_dir# ls # "manls" "ls help"to see usage of the commond; "cat .xx" to see the content of the file  
$diamond  diamond-linux64.tar.gz # check diamond is able to active
root@lyt:~/lyt_dir# ./diamond # active
Error: Syntax: diamond COMMAND [OPTIONS]. To print help message: diamond help # diamond can be used now
root@lyt:~/lyt_dir# ./diamond help # "help" check command
```
<b>Note: Diamond is avalible for use now, however, only under the dictionary "root@lyt:~/lyt_dir#", if active below other dictionary:</b>
```Bash
root@lyt:~/lyt_dir# cd ..
  
root@lyt:~# diamond
  Command 'diamond' not found, but can be installed with:
  apt install diamond-aligner
```
<b>Then, the commond cannot be found in other dictionary.</b>
<br>
Diamond and MCScanX need to be actived globally, next step is to solve this problem.
<br>
```Bash
root@lyt:~# echo $PATH # the list of directories that will be searched for anything that you type on the command line; seperate by ":"
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
  
root@lyt:~# ls
  lyt_dir
  
root@lyt:~# cd lyt_dir/
  
root@lyt:~/lyt_dir# ls
  diamond  diamond-linux64.tar.gz
  
root@lyt:~/lyt_dir# pwd # print working directory
  /root/lyt_dir
  
root@lyt:~/lyt_dir# cd /usr/local/bin
  
root@lyt:/usr/local/bin# cp -i /root/lyt_dir/diamond /usr/local/bin/ #copy diamond from "/root/lyt_dir" into "/usr/local/bin/"
  
root@lyt:/usr/local/bin# ls
  diamond
```
Now diamond can be active under any dictionary
<br><br>  
<b><2> Download MCScanX:<br></b>
```bash
root@lyt:~/lyt_dir# mkdir MCScanX #新建文档
root@lyt:~/lyt_dir# cd MCScanX/
root@lyt:~/lyt_dir/MCScanX# git clone https://github.com/wyp1125/MCScanX.git #从github下载该软件
  Cloning into 'MCScanX'...
```

  <b>Error:</b>
```bash
make[1]: Entering directory '/root/lyt_dir/MCScanX/MCScanX/downstream_analyses'
javac -g dot_plotter.java
make[1]: javac: Command not found
make[1]: *** [makefile:5: dot_plotter.class] Error 127
make[1]: Leaving directory '/root/lyt_dir/MCScanX/MCScanX/downstream_analyses'
make: *** [makefile:7: mcscanx] Error 2
```
The error happened after enter the pathway '/root/lyt_dir/MCScanX/MCScanX/downstream_analyses', so enter the file to see what's wrong
```bash
root@lyt:~/lyt_dir/MCScanX/MCScanX# cd downstream_analyses/
  
root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# ls
  
  dot_plotter.java
  dual_synteny.ctl
  dual_synteny_plotter.java
  family_circle_plotter.java
```
Many .java file there, so this error may cause by 'javac: Command not found'
```bash
root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# sudo apt update #first try update首先尝试升级
  
root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# apt list --upgradable
  Listing... Done
  
root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# java - version

  Command 'java' not found, but can be installed with:
  apt install openjdk-11-jre-headless  # version 11.0.17+8-1ubuntu2~20.04, or
  apt install default-jre              # version 2:1.11-72
  apt install openjdk-16-jre-headless  # version 16.0.1+9-1~20.04
  apt install openjdk-17-jre-headless  # version 17.0.5+8-2ubuntu1~20.04
  apt install openjdk-8-jre-headless   # version 8u352-ga-1~20.04
  apt install openjdk-13-jre-headless  # version 13.0.7+5-0ubuntu1~20.04

root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# apt install default-jre # install the java environment

root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# javac

  Command 'javac' not found, but can be installed with:
  apt install openjdk-11-jdk-headless  # version 11.0.17+8-1ubuntu2~20.04, or
  apt install default-jdk              # version 2:1.11-72
  apt install openjdk-16-jdk-headless  # version 16.0.1+9-1~20.04
  apt install openjdk-17-jdk-headless  # version 17.0.5+8-2ubuntu1~20.04
  apt install openjdk-8-jdk-headless   # version 8u352-ga-1~20.04
  apt install ecj                      # version 3.16.0-1
  apt install openjdk-13-jdk-headless  # version 13.0.7+5-0ubuntu1~20.04

root@lyt:~/lyt_dir/MCScanX/MCScanX/downstream_analyses# apt install default-jdk # install java

root@lyt:~/lyt_dir/MCScanX/MCScanX# make #active make file again 
```
This time MCSscanX is sucessfully downloaded and ready for use
  
```bash
root@lyt:~/lyt_dir/MCScanX/MCScanX# pwd
root@lyt:~/lyt_dir/MCScanX/MCScanX# cp -i /root/lyt_dir/MCScanX/MCScanX/MCScanX /usr/local/bin/
```
The diamond and MCScanX are configured for using under any dictionary.
<br><br>

  <b>3. Using SynnetBuild-X.sh for building synteny network:</b>
  <1>. Replace the array at 70 lines with own species name
  <2>. ./SynetBuild-X.sh 6 5 25 10 #top hits, anchors, upstream and downstream gene numbers for searching anchors, threads
 
  
  
  
  

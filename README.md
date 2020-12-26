# linux101





#01 Rename

cat ala.cds.fasta | awk '{ gsub(/alaSesamum_al;/, "ala_"); print }' > ala.cds.formatted.fasta


#02 split a multifasta file in each set with their corresponding header 


```

cat yourfile.fasta | awk '{
if (substr($0, 1, 1)==">") {filename=(substr($0,2) ".fasta")}
print $0 > filename }'


```

#03 make a tab separated file as in put for PREP suite online tool 

cat ind_accD.fasta | awk 'NR==2{print "indicum"}2' | awk 'NR==3{print "accD"}3' | awk 'NR==4{print "1"}4' | awk 'NR==5{print "0.8"}5'| awk '{if (NR!=1) {print}}' | awk -F'\n' '{$1=$1} 1' RS='\n\n' OFS='\t' > accD.rna.ready










- How To Count Files in Directory on Linux | [answer](https://devconnected.com/how-to-count-files-in-directory-on-linux/) | `*ls | wc -l*`


- How to gzip a folder? | answewr is [here](https://mkyong.com/linux/linux-how-to-gzip-a-folder/) | ```tar -zcvf foldername.tar.gz foldername/``` | | explanation [here](https://unix.stackexchange.com/questions/93139/can-i-zip-an-entire-folder-using-gzip) | You can confirm its contents: ```tar ztvf foldername.tar.gz ```


- #### want to extract a specifc file in a compressed file in linux? do like this for [tar](https://linuxconfig.org/how-to-extract-a-specific-file-from-gzip-compressed-archive-tarball) and like this for [gz](https://unix.stackexchange.com/questions/14120/extract-only-a-specific-file-from-a-zipped-archive-to-a-given-directory) file | `unzip -l unzipfile` then `unzip unzipfile fullpathtothefile > yourfile`


- #### want to check parent ID and PID for cleaning zombies do `ps -f -u username` then `kill yourPIDofinterest`

- ####  ps usage [1](https://superuser.com/questions/102005/how-can-i-display-the-memory-usage-of-each-process-if-i-do-a-ps-ef) | [2](https://alvinalexander.com/linux/unix-linux-process-memory-sort-ps-command-cpu/) | [3](https://alvinalexander.com/unix/man/linux-ps-man-page-ps-help/) | [4](https://www.networkworld.com/article/3516319/showing-memory-usage-in-linux-by-process-and-user.html) | [5](https://www.endpoint.com/blog/2017/08/08/how-to-check-process-duration-in-linux)

- #### [oneliners](https://github.com/stephenturner/oneliners)  | The reads that passed the base caller quality filter were then filtered with seqtk v1.3 (seqtk, RRID:SCR_018927) [19] to remove reads <10 kb (seq -A -L 10 000), yielding a final set of 1,050,302 reads with a total size of 38.2 Gb and ∼45× coverage (Supplementary Table S2). | [blog point 9](https://nbisweden.github.io/workshop-archive/workshop-genome_assembly/2017-11-15/solutions/Solutions_Data_Quality_Assessment.html)

- #### [Linux Command Line Full course: Beginners to Advance. Bash Command Line Tutorials](https://youtu.be/2PGnYjbYuUo)

- #### [7 System Monitoring Tools for Linux to Keep an Eye on Vital System Stats](https://itsfoss.com/linux-system-monitoring-tools/)

- #### CPU and Memory usage record for a multiple algorithm process

Hello everyone.

Here is a bash script for long-reads assembly using CANU.

```
#!/bin/bash 
set -e export 
PATH='/home/raymond/devel/canu/canu/Linux-amd64/bin/':$PATH 
inputFile=$1 
outputDir=$2 
name='Epau' 
genomeSize=160kb 
threads=40 
gnuplotPath=/home/raymond/devel/gnuplot/install/bin/gnuplot 
echo $inputFile 
echo $outputDir 
canu \ -p $name \ 
-d $outputDir \ 
correctedErrorRate=$correctedErrorRate \ genomesize=$genomeSize \ 
-nanopore-raw $inputFile\
 gnuplot=$gnuplotPath \ 
useGrid=false \ maxThreads=$threads 
```

I would like to incorporate a command line in order to get CPU and memort usage every 5 mn from the begining to the end of the CANU assembly.

How could I get this info in a specific file as an output since CANU running deals with a bunch of multiple processes?

Thanks.

- ##### A1 
There are lots of different ways to attack this problem.

System stats are all in files in /proc, so to get memory usage you might parse /proc/meminfo. For CPU utilization /proc/loadavg might be what you want. Here is a link to some documentation. You could write a bash script to get these values and write to a file.

You could also add in a middle man and use the psutil package for Python and just use that

There are probably lots of other ways to do this as well

- ##### A2

f its running as a systems process, firefox for example, use

top| grep firefox --line-buffered > outfile.txt
I couldn't figure out how to get my cut to work in-line though, it seems the delimiters are scrambled after field 2.

- #### A3

answer depends on OS and environment to some extent-- is this a machine with few other users or a dedicated VM, or a shared host, and what's the OS/distribution you're running?

quick and dirty would be to run top in batch mode if that's available. Reports of the host's memory usage are available via free and vmstat -- those are useful to see if your process is eating all available memory and then failing. Unlikely with such a small genome.


Thank you for your reply. I am working on Centos 7 OS.



Probably easiest is calling top -b -n 99 -s 13 or something similar with parameters appropriate to your work.

If you are hoping for a machine-readable log and a way to summariza a proces tree by a piece of code, then more work will be necessary, but this will give you output good for human eyes to understand what's happening.


A4

[git1](https://github.com/ibest/ARC/blob/master/contrib/profilemem.R)
[git2](https://github.com/ibest/ARC/blob/master/contrib/plot_memprofile.R)

[online1 | Reponse 16](https://stackoverflow.com/questions/1221555/retrieve-cpu-usage-and-memory-usage-of-a-single-process-on-linux)

[online](https://alvinalexander.com/linux/unix-linux-process-memory-sort-ps-command-cpu/)

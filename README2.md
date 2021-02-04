# Advanced Data Analysis - Introduction to NGS data analysis
## Department of Animal and Plant Sciences, University of Sheffield
#### Nicola Nadeau, Alison Wright

The aim of this course is to give an introduction to handling NGS sequence data on the UoS HPC cluster (ShARC) and to some of the analyses you might want to do focussing on investigating gene expression.


## Schedule 2021

| Content | Date | Session | Lead | TAs |
| ------- | ---- | ------- | ---- | --- |
| [Introduction to the HPC and NGS data](https://github.com/njnadeau/NGScourse/blob/master/day1am.md) | Mon 02/03/2020 | Morning (9-12) | ADB - A04 (Perak) | Nicola Nadeau | Thea Rogers, Jake Pepper, Naomi Cox |
| [Sequence data formats and assessing sequence quality](https://github.com/njnadeau/NGScourse/blob/master/day1lateam.md) | Mon 02/03/2020 | Morning (9-12) | ADB - A04 (Perak) | Nicola Nadeau | Thea Rogers, Jake Pepper, Naomi Cox |
| [Aligning Illumina RNA-seq data](https://github.com/alielw/APS-NGS-day2-AM/blob/master/README.md) | Mon 02/03/2020  | Afternoon (2-5) | ADB - A04 (Perak) | Alison Wright | Thea Rogers, Jake Pepper, Naomi Cox |
| [Differential gene expression analyses](https://github.com/alielw/APS-NGS-day2-PM/blob/master/README.md) | Wed 04/03/2020  | Afternoon (2-5pm) | ADB - A04 (Perak) | Alison Wright | Thea Rogers, Jake Pepper, Naomi Cox |
| [SNP and genotype calling](https://helenhip.github.io/SNP-and-genotype-calling/) | Fri 06/03/2020 | Afternoon (2-5pm) | ADB - A04 (Perak) | Helen Hipperson | Thea Rogers, Jake Pepper, Naomi Cox |


### General notes
Here are some websites that it is useful to have on hand (you might want to bookmark these so you can easily go back to them)

Linux and Shell cheatsheet (it's not cheating!): http://rcg.group.shef.ac.uk/courses/linux/shell-cheatsheet.html

CiCS page on using the ShARC cluster: https://www.sheffield.ac.uk/cics/research/hpc/sharc

CiCS page on interactive useage of the cluster: https://www.sheffield.ac.uk/cics/research/hpc/using/interactive

CiCS page on submitting jobs to the cluster (more on his later): https://www.sheffield.ac.uk/cics/research/hpc/sharc/batch

Documentation on file storage on ShARC http://docs.iceberg.shef.ac.uk/en/latest/hpc/filestore.html

The genomics software repository: http://soria-carrasco.staff.shef.ac.uk/softrepo/

#### Working off-campus
To access sharc from off-campus you may need to connect to the University's vpn. 

Instructions to set up the vpn: https://www.sheffield.ac.uk/it-services/vpn

#### Logging in and getting started
We will be working on windows machines, which means that you need to use a program (ssh client) to access the cluster. We will be using MobXterm. Start by opening the program, if you have used it before to connect to sharc you may find "sharc.shef.ac.uk" under "User sessions", in which case you can just double click on this to launch an ssh session on sharc. If not, click on "Session">"SSH" and enter
```
sharc.sheffield.ac.uk
```
in the "Remote host" box and specify your username (port should always be 22).

Request an interactive session:
```bash
qrsh
```
You should always start by doing this. No work should ever be done on the head node! If you are on a head node you will see someting like this in your command line prompt:
```
[bo1nn@sharc-login1 ~]$
```
This node is just a gateway to the worker nodes. If you are on a worker node you will see the name of the node, eg.
```
[bo1nn@sharc-node004 ~]$
```
#### Important note
***
This tutorial relies on having access to a number of programs. The easiest way is to have your account configured to use the Genomics Software Repository. If that is the case you should see the following message when you get an interactive session with ```qrsh```:
```
  Your account is set up to use the Genomics Software Repository
     More info: http://soria-carrasco.staff.shef.ac.uk/softrepo
```
If you don't get that message, follow the instructions [here](http://soria-carrasco.staff.shef.ac.uk/softrepo/) to set up your account.

In addition, if you want to configure the ```nano``` text editor to have syntax highlighting and line numbering, you can configure it this way:
```bash
cat /usr/local/extras/Genomics/workshops/January2018/.nanorc >> /home/$USER/.nanorc
```
***

#### Note on transferring output files to your local computer for visualization
***
You probably will want to transfer files to your own computer for visualization (especially the images). If you are working on a windows machine and using MobaXterm then the easiest option is to use the graphical sftp panel on the left, using the icons or dragging and dropping from your computer. 

Another possibility is to email the files, for example:
```bash
echo "Text body" | mail -s "Subject: gemma - hyperparameter plot" -a /data/myuser/gwas_gemma/output/hyperparameters.pdf your@email
```

In Linux and Mac, you can use rsync on the terminal. For example, to transfer one of the pdf files or all the results that are generated in this practical, the command would be: 
```bash
# transfer pdf file
rsync myuser@iceberg.sheffield.ac.uk:/data/myuser/gwas_gemma/output/hyperparameters.pdf ./
# transfer all results
rsync -av myuser@iceberg.sheffield.ac.uk:/data/myuser/gwas_gemma/output ./
```

Other graphical alternatives are [WinSCP](http://dsavas.staff.shef.ac.uk/software/xconnect/winscp.html), [Filezilla](https://filezilla-project.org/) or [Cyberduck](http://www.macupdate.com/app/mac/8392/cyberduck). You can find more detailed information [here](https://www.sheffield.ac.uk/wrgrid/using/access).

***


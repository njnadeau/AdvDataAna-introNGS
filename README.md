# Advanced Data Analysis - Introduction to NGS data analysis
## Department of Animal and Plant Sciences, University of Sheffield
#### Nicola Nadeau, Alison Wright

The aim of this course is to give an introduction to handling NGS sequence data on the UoS HPC cluster (ShARC) and to some of the analyses you might want to do focussing on investigating gene expression.


## Schedule 2024

| Content | Date | Lead | TAs |
| ------- | ---- | ---- | --- |
| [Introduction to the HPC and NGS data](https://github.com/njnadeau/NGScourse/blob/master/day1am.md) | Mon 17/02/2025 | Nicola Nadeau | Noah Bourne, Cat Collins |
| [Sequence data formats and assessing sequence quality](https://github.com/njnadeau/NGScourse/blob/master/day1lateam.md) | Tues 18/02/2025 | Nicola Nadeau | Noah Bourne, Cat Collins |
| [Aligning Illumina RNA-seq data](https://github.com/njnadeau/APS-NGS-day1-PM/blob/patch-2/README.md) | Fri 21/02/2025  | Nicola Nadeau | Noah Bourne, Cat Collins |
| [Differential gene expression analyses](https://github.com/alielw/APS-NGS-day2-PM/blob/master/README.md) | Extension (not covered or assessed)  | |  |
| [SNP and genotype calling](https://helenhip.github.io/SNP-and-genotype-calling/) | Extension (not covered or assessed) | 


### General notes
Here are some websites that it is useful to have on hand (you might want to bookmark these so you can easily go back to them)

UNIX tutorial: https://swcarpentry.github.io/shell-novice/

Documentation on using the HPC systems: https://docs.hpc.shef.ac.uk/en/latest/hpc/index.html

#### Working off-campus
To access the HPC from off-campus you may need to connect to the University's vpn. 

Instructions to set up the vpn: https://www.sheffield.ac.uk/it-services/vpn

#### Logging in and getting started
If you are working on a Windows machine For Windows PCs, we recommend the use of Windows Terminal which is available on the University’s managed desktops by default. If not already installed on your device, Windows Terminal can be found on the Microsoft Store. If you are using a different operating system there are instructions [here](https://docs.hpc.shef.ac.uk/en/latest/hpc/connecting.html#suggested-ssh-clients&gsc.tab=0). Start by opening the terminal, then run the following command to log in to bessemer
```
ssh -X YOUR_USERNAME@bessemer.shef.ac.uk
```
specify your username. You will then be prompted for dual-factor authentication.

Access a worker node:
```bash
srun --pty bash -l
```
You should always start by doing this. No work should ever be done on the head node! If you are on a head node you will see someting like this in your command line prompt:
```
[bo1nn@bessemer-login1 ~]$
```
This node is just a gateway to the worker nodes. If you are on a worker node you will see the name of the node, eg.
```
[bo1nn@bessemer-node004 ~]$
```
***
#### Accessing reserved training resources on Bessemer
***
If you find you are waiting a long time for your jobs to start running or to get access to an interactive session you can try the following:
For interactive sessions
```bash
srun --account=ngscourse --pty bash -l
```
For batch jobs, add the following to the header section of your batch job file
```
#!/bin/bash
#SBATCH --account=ngscourse
```
***
#### killing processes and stopping jobs
***
To kill a running interactive command: ctrl + C

If you start a job running but find a mistake or decide you want to cancel it, you can cancel jobs with ```scancel job-id```
***
#### Important note
***
This tutorial relies on having access to a number of programs. The easiest way is to have your account configured to use the Genomics Software Repository. If that is the case you should see the following message when you get an interactive session with ```srun --pty bash -l```:
```
  Your account is set up to use the Genomics Software Repository
```
The first excerises go though setting this up.

In addition, if you want to configure the ```nano``` text editor to have syntax highlighting and line numbering, you can configure it this way:
```bash
cat /shared/genomicsdb2/shared/workshops/January2018/.nanorc >> /home/$USER/.nanorc
```
***
#### Note on transferring output files to your local computer for visualization
***
You probably will want to transfer files to your own computer for visualization (especially the images). Perhaps the easiest option is to use [SCP](https://docs.hpc.shef.ac.uk/en/latest/hpc/transferring-files.html) from the terminal and this is what we will use in the practicals. 

Another possibility is to email the files, for example:
```bash
echo "Text body" | mail -s "Subject: gemma - hyperparameter plot" -a /data/myuser/gwas_gemma/output/hyperparameters.pdf your@email
```

In Linux and Mac, you can use rsync on the terminal. For example, to transfer one of the pdf files or all the results that are generated in this practical, the command would be: 
```bash
# transfer pdf file
rsync myuser@bessemer.sheffield.ac.uk:/data/myuser/gwas_gemma/output/hyperparameters.pdf ./
# transfer all results
rsync -av myuser@bessemer.sheffield.ac.uk:/data/myuser/gwas_gemma/output ./
```

Other graphical alternatives are [WinSCP](http://dsavas.staff.shef.ac.uk/software/xconnect/winscp.html), [Filezilla](https://filezilla-project.org/) or [Cyberduck](http://www.macupdate.com/app/mac/8392/cyberduck). You can find more detailed information [here](https://www.sheffield.ac.uk/it-services/research/hpc/using/access).

***


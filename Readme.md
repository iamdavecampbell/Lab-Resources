---
title: "Lab Manual"
author: "Dave Campbell"
date: "2024-12-19"
output: html_document
---



## Github

Github is a collaborative tool that lets us review and modify code.

Initial work can be from your own github repo. When the work gets far enough along you will be asked to change to a repo under [https://github.com/iamdavecampbell](https://github.com/iamdavecampbell)
your commits etc still show up as having been attributed to you.  Moving the repo ensures longer term development.

You are expected to commit/push changes regularly so that we can collaborate and your code can be tested and reviewed.

Within your repo your **Readme.md** file should list the main files and what they do.  

Scripts should be organized using best coding practices and following the coding templates.

- R_Markdown_obtain_and_prepare_CanSim_files_from_StatCan 
- Python_Markdown_obtain_and_prepare_CanSim_files_from_StatCan



## Overleaf
Overleaf is a collaborative writing tool that uses LaTeX 
Manuscripts including comprehensive exam literature review, papers in progress etc will be housed on Overleaf and kept up to date.  This allows us to track changes when needed and check work.



## Using Servers

- Replace **USERNAME** with _campbell_ or whatever your given username might be.
- Replace **SERVERNAME** with the machine name.  

Both will be provided as needed.  You will need ot change your password the first time tyou log into the machine.  

### Running code: 


**SSH** is a secure shell tool for running code in the command line / terminal on a remote machine.  You write the code on your machine and it runs and saves output on mine.

To log into my machine use:

- **ssh USERNAME@SERVERNAME**

Your home directory should be located on **/home**. To determine your _present working directory_ use this

- pwd

To see the machines CPU and free memory resource use try:

- top

To get out of top you type 'q' otherwise it will continue to monitor for eternity.

To see the machines GPU resource use try this to get a snapshot of the current use:

- nvidia-smi


You can run R via command line with:

- R

You can open python via command line with one of these:

- python
- python3.9


If you want to submit a job for remote work I usually use the **nohup** so that the code keeps running even if my internet connection breaks.  In the command line it looks like this:

- nohup python script_2_run.py > Name_of_logfile_that_you_can_check_for_output.txt &

- nohup Rscript script_2_run.R > Name_of_logfile_that_you_can_check_for_output.txt &

Or provide some R code before or instead of running the script using **-e** and being careful about the brackets.

- nohup Rscript -e "some_R_code_goes_here; some_more_R_code;source('script_2_run.R')" > Name_of_logfile_that_you_can_check_for_output.txt &




### Moving files back and forth:

Transferring files between machines can be done using **rsync** or **scp** but for most people it's easy to  accidentally overwrite something important using those.  

- Use a file transfer program.  Use an open source tool like: **FileZilla** [https://filezilla-project.org](https://filezilla-project.org)

Use your same username.  The host needs some added care.  Use a secure file transfer protocol so that it the host box looks like this:

- sftp://SERVERNAME


This will let you drag and drop files between your machine and the server using an easy user interface with simplified, easy to read rules for handling conflicts.


### Port Forwarding

To Use Jupyter as a development environment you'll need to use port forwarding so that code is written on your (local) machine but the code is run on the (remote) server.  Output and plots will be brought back to your local machine.

You'll need two terminal windows.  In terminal 1: SSH into the remote host using something like

- ssh USERNAME@SERVERNAME

In terminal 1: Choose a 4 digit port number, say **<port_number>**, this is the port that will be monitored by jupyter to bring results from the remote server to your local machine.  Include the port number like this:

- jupyter notebook --no-browser --port=<port_number> --ip=0.0.0.0

This will give you a token which you will need when you get into the notebook

In terminal 2: In a second terminal map your local machine and the remote machine by creating a ssh tunnel:

- ssh -L   localhost:<port_number>:localhost:<port_number> USERNAME@SERVERNAME

Then point at web browser at the address from terminal 1.  It’ll be something like
http://0.0.0.0:1234/?token=30bc7f399df2q7da463d0673b7420ds741abacf596d3fbe....





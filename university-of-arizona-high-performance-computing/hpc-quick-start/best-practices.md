# Best Practices

## Overview <a href="#bestpractices-overview" id="bestpractices-overview"></a>

You share Ocelote, ElGato, and Puma with many other users and what you do can affect others. Exercise good citizenship to ensure that your activity does not adversely impact the system and the research community with whom you share it. Below are some rules of thumb.

## Login Nodes <a href="#bestpractices-loginnodes" id="bestpractices-loginnodes"></a>

A login node serves as a staging area where you can perform housekeeping work, edit scripts, and submit job requests for execution on one/some of the cluster’s compute nodes. It is important to know that the login nodes are not the location where scripts are run. Heavy computation on the login nodes slows the system down for all users and will not give you the resources or performance you need. It should also be stressed that software is not available on the login nodes. General practices:

1. **Know when you are on a login node**.  You can use your Linux prompt or the "hostname" command. It is where you land when you choose `shell` from the bastion node. To differentiate, the bastion host (gatekeeper, or keymaster) is a secure portal from the outside and serves no compute function.
2. **Appropriate activities**: edit and manage files, request interactive sessions, submit jobs, and track jobs.
3. **Avoid computationally intensive activity**.\
   a. Don't run research applications.  Use an interactive session if running a job is not appropriate.\
   b. Don't launch too many simultaneous processes.  \
   c. That script you run to monitor job status several times a second should probably run every few minutes.\
   d. I/O activity can slow the login node for everyone, like multiple copies or "ls -l" on directories with 000's of files.

## Shared File System <a href="#bestpractices-sharedfilesystem" id="bestpractices-sharedfilesystem"></a>

The shared file system is the location for everything in /home, /xdisk, and /groups. The exception is /tmp which is the local disk on each node. Your I/O activity can have dramatic activity on other users. The general statement here is to ask the consultants for advice on improving your I/O activity. The time spent can be saved many times over in faster job execution.

1. **Use /tmp for working space**. If you have multiple jobs that will use the same data, there are ways to copy it to /tmp and run multiple jobs dramatically increasing performance and reducing I/O load.
2. **Be aware of I/O load**. If your workflow creates a lot of I/O activity then creating dozens of jobs doing the same thing may be detrimental.
3. **Avoid storing many files in a single directory**. Hundreds of files is probably ok; tens of thousands is not.
4. **Avoid opening and closing files repeatedly in tight loops.**  If possible, open files once at the beginning of your workflow / program, then close them at the end.
5. **Watch your quotas**.  You are limited in capacity and file count. Use "uquota". In /home the scheduler writes files in a hidden directory assigned to you.
6. **Avoid frequent snapshot files** which can stress the storage.
7. **Limit file copy sessions**. You share the bandwidth with others.  Two or three scp sessions are probably ok; >10 is not.
8. **Consolidate files**. If you are transferring many small files consider collecting them in a tarball first.
9. **Use parallel I/O** if available like "module load phdf5"

## Submitting Jobs <a href="#bestpractices-submittingjobs" id="bestpractices-submittingjobs"></a>

1. **Don't ask for more time than you really need.**  The scheduler will have an easier time finding a slot for the 2 hours you need rather than the 48 hours you request.  When you run a job it will report back on the time used which you can use as a reference for future jobs. However don't cut the time too tight.  If something like shared I/O activity slows it down and you run out of time, the job will fail.
2. **Test your submission scripts.**  Start small. You can use an [interactive session](https://confluence.arizona.edu/pages/viewpage.action?pageId=93160866#RunningJobswithSLURM-Interactivecommand) to help build your script and run tests in real time.
3. **Respect memory limits.**  If your application needs more memory than is available, your job could fail and leave the node in a state that requires manual intervention.
4. **Do not run scripts automating job submissions.** Executing large numbers of job submissions in rapid succession (e.g. in a scripted loop) can overload the system's scheduler and cause problems with overall system performance. A better alternative is to submit job arrays.
5. **Hyperthreading is turned off**.  Running multiple threads per core is generally not productive.  MKL is an exception to that if it is relevant to you.

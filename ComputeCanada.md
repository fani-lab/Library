# Tips to Setup Your First Project on ComputeCanada as a Student

> First, you need an account to start using Compute Canada.
## Create an account 
Click [here](https://ccdb.computecanada.ca/account_application) and do it as follows:
1. Confirm agreement to some policies and terms of use. (Last one is _Consent to Access User Data_ that you have the choice to not consent).
2. Then select `No` in the next step: 
<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227581926-66e8e924-1630-4e1a-a592-91e179fcfac1.png"  width="600" height="400">
</p>

3. Enter your personal information:
<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227584074-6b5b29c7-e8ab-4063-b474-7ba3ba4713a6.png"  width="600" height="300">
</p>

4. Then, enter your institution information: 
<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227585750-a0dfd05a-bc55-4bd2-8b01-9e8de2df7165.png"  width="600" height="400">
</p>

**Note**: As a student, you must enter the CCRI of your sponsor or supervisor. They will be asked to confirm your role. Your sponsor can find their CCRI on their login page at [https://ccdb.computecanada.ca/](https://ccdb.computecanada.ca/). A CCRI is an identifier of the form `abc-123-01`.

5. Final step is determining a username and password:

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227587778-2fbfe34a-0277-4744-a809-0ce14b1dfadc.png"  width="600" height="400">
</p>



> Now, you can sign in.
## Login
1. Sign in with your username and password.

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227589500-338f9bde-4756-4b7b-84ba-ae8466972246.png"  width="600" height="300">
</p>

2. The Resources and Allocations can be found in `My Account > My Resources and Allocations`:
<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227591824-f84d571d-6140-4824-a109-311d03b9da63.png"  width="800" height="100">
<br/>
<img src="https://user-images.githubusercontent.com/38455739/227592513-503d3b17-0f3f-4f45-9d56-0d1d662bfc13.png"  width="200" height="300">
</p>

If you are not a student: There will be a couple of computing servers (clusters) with different names and their specifications can be found [here](https://cc.sillmedia.com/services/computing-services/clusters/). Proper choice should be made based on their technical details etc.



> Then you want to connect to your available servers.
## Connect to Servers
There are two ways to connect to a server:
1. Traditionally use _SSH_ and Windows command prompt or Linux's terminal. Host address (or remote host) will be `{name_of_the_server}.computecanada.ca`  and the username/password is the same as your account. 
2. There are tools that make this process easier by providing GUI and other features. Our choices are [_MobaXterm_](https://mobaxterm.mobatek.net/) for SSH client and [_WinSCP_](https://winscp.net/eng/index.php) for file transferring ([_FileZilla_](https://filezilla-project.org/) is also a good choice). 

Here is a simple instruction of how to use [_MobaXterm_](https://mobaxterm.mobatek.net/download.html) for connecting to a server:

1. Open a session by clicking `session button` on the top left corner as follows:

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227680488-774403ca-aa30-46d5-8e4f-3c2107d99d7b.png"  width="600" height="100">
</p>

2. Click `SSH button`.

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227680481-7a97d204-0f59-4ee6-b17c-0349082125e1.png"  width="600" height="400">
</p>

3. Enter your `Remote Host` and `Username` as follows:

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227680492-67cb0174-0d31-43ed-aad3-f9c46d9419d6.png"  width="600" height="400">
</p>

4. click `OK`.

5. Enter your Username and Password if requested in the opened terminal.

Before Deploying the project, you need to upload your project files to the server.

Most of the servers have a projects directory. Using _MobaXterm_, after connecting to the server, you can open it and upload your files with `drag and drop` or via `upload buttons`.

We recommend using [_WinSCP_](https://winscp.net/eng/download.php) especially if your files are huge. It will be also helpful when you want to download the outputs too.

Here is a simple instruction of how to use [_WinSCP_](https://mobaxterm.mobatek.net/download.html) for connecting to a server for transferring your files:

1. After opening the app, click on the `New Session` button or click `session` on the navigation bar and then select `New Session`. (You can also use this shortcut: `Ctrl+N`)

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227682413-e57ae395-a02e-44a4-88ac-dbd8ef7de65a.png"  width="600" height="400">
</p>

As you can see on the left side you have your system directories.

2. Enter your `Remote Host`, `Username`, and `Password` and then click `Login` as follows:

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227689340-ba9d300b-9bd8-41ae-b7a9-be7842ac6a96.png"  width="600" height="400">
</p>

3. After connection, you have the server files and directories on the right side. So, you can transfer your files between your system and server or vice versa.

<p align="center">
<img src="https://user-images.githubusercontent.com/38455739/227689947-497269d9-d2d2-4098-8246-3b32eb578248.png"  width="600" height="400">
</p>



> Now that you are connected to the server, and ready to enter your commands, it's time to deploy your project on the server.

## Deploy Project

For making your project available on server, ready to run and utilize, after uploading the project to the server of choice, you must _create a virtual environment_:

1. First, you have to choose a Python version to load, based on your project and supported versions by _Compute Canada_. List of the supported versions is available [here](https://docs.alliancecan.ca/wiki/Python#Loading_an_interpreter).
Also, you can get it by this command: 
```
[name@server ~]$ module avail python
```
2. Load desired python version (e.g., 3.10): 
```
[name@server ~]$ module load python/3.10 
```
3. Create a virtual environment using Python module that you loaded (`project_name_env` is the name of the directory for your new environment): 
```
[name@server ~]$ virtualenv --no-download {project_name_env}
```
4. Activate the virtual environment: 
```
[name@server ~]$ source {project_name_env}/bin/activate
```
5. Upgrade pip in the environment: 
```
[name@server ~]$ pip install --no-index --upgrade pip
```
6. Exit the virtual environment, simply enter the command deactivate: 
```
({project_name_env}) [name@server ~] deactivate 
```
7. You can now use the same virtual environment over and over again. Each time: 
    1. Load the same environment modules that you loaded when you created the virtual environment, e.g: `module load python scipy-stack`
    2. Activate the environment: `source {project_name_env}/bin/activate`

**Note:** Although you might experience many timeouts while uploading or working with clusters using the university's network, the best setting based on my experience is using VPN on securelogin, and external. 

> You should do the above steps as a necessary task for deploying your project. However, there is no need to redo them each time you want to execute your code. The following part shows how to run your code on the server as a job.

## Execute Project
To submit your project as a job to the server, you have to specify the time and other resources you need in a bash script. For example: 

```
#!/bin/bash 


##setup the environment

module load python/3.8; 

module load scipy-stack; 

source {project_name_env}/bin/activate; 

pip install --no-index --upgrade pip; 
 

# SBATCH --time=20:00:00 

# SBATCH --account=def-hfani 

# SBATCH --gpus-per-node=2 

# SBATCH --mem=64000M 

# SBATCH --mail-user=hfani@uwindsor.ca 

# SBATCH --mail-type=ALL 
 

python main.py -arg0 ‘argv0’ 
```

**Note:** If you want to download from the internet, Remove the -–no-index when installing pip modules. The -–no-index refer to you not using any index to fetch your modules except the ones provided by _Compute Canada_.

***IMPORTANT NOTE:*** _Some bash commands should be entered in the command line instead of the bash file to affect the result._ Read the **Submit Job** section for more information.

Refer [here](https://docs.alliancecan.ca/wiki/Running_jobs) for detailed explanations and examples.

### Submit Job

To request for the resources and schedule a job for execution:

```
[name@server ~]$ sbatch computecanada.sh
```

As we metioned, _Some bash commands should be entered in the command line instead of the bash file to affect the result._

For example, if you want to run a job with `40 cpus`, `20 hour` time limit, `64GB ram`, and you want to get your email notifications to `johndoe@uwindsor.ca` you have to use this command (if the name of your bash file is computecanada.sh): 

```
[name@server ~]$ sbatch --time=20:00:00 --mem=64000M --mail-user=johndoe@uwindsor.ca --mail-type=ALL --cpus-per-task=40 computecanada.sh 
```

If you want to use GPU instead, you have to use `--gpus-per-node=2` (if you want 2 GPUs).

Certainly, you should first check whether gpu is available. For example, if you use _torch_, you can use `torch.cuda.is_available()` as a manual check.

We will add our experience of executing project on gpu on Compute Canada here, soon.



> Finally, you are executing your project on the server as a job. The next issue is that you are curious about the status of the job or the output and results. So, you need to know how to monitor progress.

## Monitor Progress
After submitting a job, you can monitor the progress and results with different tools.

### Check Status
The general command for checking the status of _Slurm_ jobs is `squeue`, but by default it supplies information about _all_ jobs in the system, not just your own. You can use the shorter `sq` to list only your own jobs:
```
$ sq
  JOBID    USER     ACCOUNT     NAME      ST   TIME_LEFT   NODES  CPUS    GRES     MIN_MEM    NODELIST (REASON) 

  123456   smithj   def-smithj  simple_j  R    0:03        1      1       (null)   4G cdr234  (None) 

  123457   smithj   def-smithj  bigger_j  PD   2-00:00:00  1      16      (null)   16G        (Priority)
```

The `ST column` of the output shows _the status of each job_. The two most common states are `"PD"` for "pending" or `"R"` for "running".

### Using Multiprocessing Module in Python
Compute Canada servers run with Linux which by default uses the fork method to run your multiprocessing. This should be of no problem if you are running independant methods. But when passing partial for computation, you need to have `spawn` method enabled. Its a best practice to fetch the number of cpus from the environmental variables stored in the compute nodes rather than specifying them manually

Example python code to call a search method for retrieval computation:

``` python
from multiprocessing import freeze_support,get_context
ncpus = int(os.environ.get('SLURM_CPUS_PER_TASK',default=1))
...

if __name__ == '__main__':
    freeze_support()
    mp.set_start_method('spawn')
    with get_context('spawn').Pool(ncpus) as p:
      p.starmap(partial(search, ranker=ranker, topk=topk, batch=settings['batch']),file_changes)
```


### Output
By default the output is placed in a file named `"slurm-"`, suffixed with the `job ID number` and `".out"`, e.g. _slurm-123456.out_, **in the directory from which the job was submitted**. Having the job ID as part of the file name is convenient for troubleshooting. A different name or location can be specified if your workflow requires it by using the `--output` directive.

_Slurm_ files are similar to log files, you can examine those in order to find issues or track the output of your program. 

**Helpful Command:** You can use `tail` command to read _the last part of our log file_. For example, to read last 50 lines of _slurm-123.out_ you can use the following command:
```
[name@server ~]$ tail -f -n 50 slurm-123.out 
```

 

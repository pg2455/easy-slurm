# easy-slurm

[SLURM workload manager](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is used widely to schedule jobs on the server.
The service is used by several users, and it can be time consuming to know the useful commands.
I have been using some of these commands quite frequently to monitor jobs and notify via app notifications when the jobs are finished.
It prevents a lot of work interruption, because I only have to check the server once I get a notification. 


## Installation

Note: An environment variable `$USER` is assumed to be available. This variable will be used to check for the jobs in the queue. For example, `squeue -u $USER`

1. Clone this repo in your `~/bin` directory, and add this to your `$PATH`.

```bash
mkdir ~/bin && cd ~/bin && git clone https://github.com/pg2455/easy-slurm.git && cd ~
echo "export PATH=$PATH:~/bin/easy-slurm" >> ~/.bashrc
source ./.bashrc
```

2. (optional) To setup notifications using [IFTT](https://ifttt.com/), follow these steps -
    1. Make an account on IFTT (https://ifttt.com/)
    2. [instructions](https://sungkhum.medium.com/how-to-easily-push-notifications-to-your-phone-from-a-micropython-device-21d39968e05c)
    3.

1. To use these commands, add these variables to your `~/.bashrc` -

```bash
export JOB_LOG_DIR=/home/pratgupt/scratch/job_logs # path where you store your logs. check `more_jobs` for its usage.
export IFTT_KEY=bWbfU3onmGUzRU3B-DVmH- # (optional)
export SERVER_NAME=beluga # (optional) server name needed for notificaitons. Its useful if you are pushing notifications from several servers.
```

If you are in a `tmux` screen, don't forget to source this bash script using `source ./bashrc`.

## Commands


| Commands          | Usage               | Description         |
| count_jobs        | count_jobs          | Counts the total number of jobs in the queue         |
| Commands          | Usage               | Description         |
|   |   |   |
Following are the commands -

count_jobs
kill_all_jobs
more_job
tail_job


notify
job_monitor
queue_monitor

## Contributing

These commands can make is easy for novices to easily manage their jobs.
As I learn more, I intend to add to this list of commands.
If you regularly use them in your workflow, I will love to know.
Please feel free to submit a PR with a command (and modified `README.md`) that makes your workflow easy.

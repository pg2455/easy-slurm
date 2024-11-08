# easy-slurm

[SLURM workload manager](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is used widely to schedule jobs on servers. Managing and monitoring jobs with SLURM can be time-consuming, especially when you're waiting for job completion notifications. This repository provides a set of easy-to-use bash scripts for SLURM to streamline job monitoring and notifications using **Telegram**, preventing workflow interruptions by notifying you only when jobs finish.

## Installation

> Note: An environment variable `$USER` is assumed to be available. This variable will be used to check for the jobs in the queue (e.g., `squeue -u $USER`).

1. Clone this repo into your `~/bin` directory, and add it to your `$PATH`.

    ```bash
    mkdir ~/bin && cd ~/bin && git clone https://github.com/pg2455/easy-slurm.git && cd ~
    echo "export PATH=$PATH:~/bin/easy-slurm" >> ~/.bashrc
    source ~/.bashrc
    ```

2. **Set up notifications using Telegram**:
    1. Create a Telegram bot by messaging [BotFather](https://core.telegram.org/bots#botfather) on Telegram.
    2. Follow the steps to get your bot's token.
    3. Send any message to the bot, then get your **chat ID** by visiting `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates` and looking for your chat `"id"` in the JSON response.
    4. Add the bot token and chat ID to your `~/.bashrc` for notifications:

    ```bash
    export TELEGRAM_BOT_TOKEN="your_bot_token_here"
    export TELEGRAM_CHAT_ID="your_chat_id_here"
    ```

3. To use these commands, you can also add the following optional environment variables to `~/.bashrc`:

    ```bash
    export JOB_LOG_DIR=/home/pratgupt/scratch/job_logs # path where you store your logs (used in `more_jobs`)
    export SERVER_NAME=beluga # (optional) server name for notifications, useful if you're pushing from multiple servers
    ```

   After making these changes, source your bash script:

   ```bash
   source ~/.bashrc
   ```

> **Note**: If you are using a `tmux` screen, ensure you source the script in each new session by running `source ~/.bashrc`.

## Commands

| Command           | Usage               | Description                                                 |
|-------------------|---------------------|-------------------------------------------------------------|
| `count_jobs`      | `count_jobs`        | Counts the total number of jobs in the queue                |
| `kill_all_jobs`   | `kill_all_jobs`     | Cancels all your jobs in the queue                          |
| `more_job`        | `more_job <job_id>` | Displays detailed information for a specific job            |
| `tail_job`        | `tail_job <job_id>` | Shows the tail of a specific job’s log file                 |
| `notify`          | `notify`            | Sends a test notification to verify the Telegram setup      |
| `job_monitor`     | `job_monitor`       | Monitors active jobs and sends a Telegram notification when they complete |
| `queue_monitor`   | `queue_monitor`     | Periodically checks the job queue and reports status changes |

> **Tip**: If you want to be notified when *all jobs* are finished, use:
>
> ```bash
> queue_monitor 0 &
> ```


> **Tip**: If you want to be notified when job with certain keywords are finished, use:
>
> ```bash
> job_monitor <keyword> &
> ```

This will allow you to continue working while receiving a notification when all jobs in the queue have completed.

These commands are designed to simplify common SLURM tasks, making it easier to monitor and manage jobs with minimal manual checking.

## Contributing

These scripts are intended to help users quickly and easily manage SLURM jobs. If you find them useful or have ideas for additional commands, I’d love to hear from you! Please feel free to submit a PR with new commands (and an updated `README.md`) that improve the SLURM workflow.
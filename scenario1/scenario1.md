Scenario: "Saint John": what is writing to this log file?

Level: Easy

Type: Fix

Tags:

Description: A developer created a testing program that is continuously writing to a log file /var/log/bad.log and filling up disk. You can check for example with `tail -f /var/log/bad.log`.
This program is no longer needed. Find it and terminate it.

Test: The log file size doesn't change (within a time interval bigger than the rate of change of the log file).

# Solution

To resolve this issue first I had to find which process is writing to the `/var/log/bad.lof file`
I used the `lsof` command to identify the process. What this commaind does is list the open files and what process has this file open for writing

`sudo lsof /var/log/bad.log`

The output of the command is shown below

![scenario1](/assets/scenario1.png)

The output of `lsof` displays the process ID (PID) and the name of the program. In this case the PID is `592`

I then went on to terminate the process with the `kill` command

`kill 592`

To verify that the process is terminated I checked that the lof file is no longer being written too with the `tail` command

`tail -f /var/log/bad.log`

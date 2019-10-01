# Robocopy – Scheduling regular file sync on change detection

There are multiple ways you can set robocopy to synchronize folders, a typical way is to create a batch file and set it to run on user start up. However an easier way is to set it up as a scheduled task.



First thing first, we will need to create a robocopy job file (e.g c:\robocopy.rcj) which contains the instructions to robocopy on what is needed

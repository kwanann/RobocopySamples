# Robocopy – Scheduling regular file sync on change detection

There are multiple ways you can set robocopy to synchronize folders, a typical way is to create a batch file and set it to run on user start up. However an easier way is to set it up as a scheduled task.


## Creating the robocopy job file
First thing first, we will need to create a robocopy job file (e.g c:\robocopy.rcj) which contains the instructions to robocopy: [sample robocopy.rcj](robocopy.rcj)

In the example robocopy, a few things are pre-configured
- Source Directory: /SD
- Destination Directory: /DD
- Copy Subdirectories: /S
- Monitor source and run again when at least 1 file has changed: /MON:1
- MIrror destination with source: /MIR
- Retry options: /R:1 /W:1

In order to run this command, we just need to trigger robocopy /job:c:\robocopy.rcj

## Creating a task inside task scheduler
The problem with running robocopy in user space is that the user will see a login prompt which isnt very nice. What needs to be done next is to move it to a scheduled task so that the user does not see the prompt. You can also use task scheduler to login as another user if there is a need to access an external file source/destination

1. Run Task Scheduler
2. Click Create Basic Task

![Step 2](https://github.com/kwanann/RobocopySamples/blob/master/Step%2002%20-%20Create%20Basic%20Task.png)

3. asdsa

![Step 3](https://github.com/kwanann/RobocopySamples/raw/master/Step%2003%20-%20Task%20Info.png)

4. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2004%20-%20Trigger.png)

5. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2005%20-%20Trigger%20Daily%20Info.png)

6. asdsa

[Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2006%20-%20Action.png)

7. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2007%20-%20Start%20a%20Program%20Info.png)

8. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2008%20-%20Finish.png)

9. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2009%20-%20Job%20-%20General.png)

10. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2010%20-%20Job%20-%20Triggers.png)

11. asdsa

![Step](https://github.com/kwanann/RobocopySamples/raw/master/Step%2011%20-%20Job%20-%20Settings.png)

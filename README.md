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

3. Enter basic information about the task

![Step 3](https://github.com/kwanann/RobocopySamples/raw/master/Step%2003%20-%20Task%20Info.png)

4. Create a **daily** trigger

![Step 4](https://github.com/kwanann/RobocopySamples/raw/master/Step%2004%20-%20Trigger.png)

5. Setup the daily trigger to start at **12am** every day, **across time zones**

![Step 5](https://github.com/kwanann/RobocopySamples/raw/master/Step%2005%20-%20Trigger%20Daily%20Info.png)

6. Select **Start a program**

![Step 6](https://github.com/kwanann/RobocopySamples/raw/master/Step%2006%20-%20Action.png)

7. Select **robocopy.exe** as the program to start and add the arguments: **/job:c:\robocopy.rcj**

![Step 7](https://github.com/kwanann/RobocopySamples/raw/master/Step%2007%20-%20Start%20a%20Program%20Details.png)

8. Check **Open the Properties dialog for this task when I click Finish** and click **Finish**

![Step 8](https://github.com/kwanann/RobocopySamples/raw/master/Step%2008%20-%20Finish.png)

9. Decide whether you wish to *Run with highest privileges*, additionally if there is a need to connect to an external file share, do update the user account this task runs as. Optionally you can also choose to select *Run whether user is logged on or not* especially if you are using an external account

![Step 9](https://github.com/kwanann/RobocopySamples/raw/master/Step%2009%20-%20Job%20-%20General.png)

10. This is a crucial screen, you will want to edit the trigger to ensure a few things.
* The task is repeated every **X hours**
* Check **Stop all running tasks at end of repetition duration**
* Check **Stop task if it runs longer than X hours**
This will ensure that robocopy is triggered and re-run every X hours

![Step 10](https://github.com/kwanann/RobocopySamples/raw/master/Step%2010%20-%20Job%20-%20Triggers.png)

11. In the final screen, you also need to setup a few options
* Failsafe: **Stop the task if it runs longer than 1 day**
* Close existing task if any by selecting **stop the existing instance**

![Step 11](https://github.com/kwanann/RobocopySamples/raw/master/Step%2011%20-%20Job%20-%20Settings.png)

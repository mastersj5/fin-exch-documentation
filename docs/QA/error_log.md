# __Iceberg Error Log__

#### Author: Luis Enrique Rodriguez

## __Table of Contents__
1. [Docker Desktop Troubleshooting](#docker-desktop-troubleshooting)
    * [Problem](#problem)
    * [Solution](#solution)
2. [Error 2: ](#error-2)
    * [Problem](#problem-1)
    * [Solution](#solution-2)
3. [Error x: ](#error-x)
    * [Problem](#problem-1)
    * [Solution](#solution-2)

## __Docker Desktop Troubleshooting__

### _Problem_

Upon opening Docker Desktop, a prolonged loading screen prevented me from accessing the app:

![](/docs/QA/error_log_files/Docker_Loading.png)

After a few minutes, this error message was displayed:

![](/docs/QA/error_log_files/WSL_error_message.png)

### _Solution_

Changing the default wsl from ubuntu to docker-desktop and restarting your pc boots up the Docker Desktop successfully.

![](/docs/QA/error_log_files/Command_Prompt_Default_WSL.png)

## __Iceberg UI Malfunction__
### _Problem_

When running the Iceberg UI and Start of Day Loader Microservices, the login and register sites will not follow through the login and show the following pop-up:

![](/docs/QA/error_log_files/Localhost_Dropdown.png)

Any attempt at interacting with the pop-up doesn't change anything and pressing the "Sign In" button does nothing. Pressing the "Cancel" button shows this error:

![](/docs/QA/error_log_files/UI_error_message.png)

### _Solution_

Run a command prompt as an administrator and run the following command:

![](/docs/QA/error_log_files/cmd_Command_Prompt_netstat.png)

The prompt will show you all currently used ports and what's running on those ports. Find the port that (in our case) is running on 8080 and run the following command:

![](/docs/QA/error_log_files/cmd_Command_Prompt_taskkill.png)

Replace "< PID >" with the port number next to 8080 and try running the microservices again. 

## __Error x__
### _Problem_
### _Solution_

#### Notes (Will be deleted later)
Look at:
* [start of day loader]
* [event stream sequencer]
* [event logger]
* [data warehouse]
* [ICE-11 test registering a user]
* [iceberg ui (later)]
* Create User Guide
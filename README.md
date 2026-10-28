
# Linux Daemon Process

A Linux system programming project in C that demonstrates daemon creation, background execution, process management, and activity logging in Ubuntu Linux.

📖 Table of Contents

.📌 Project Overview
.🎯 Objectives
.🔄 Daemon Process Flow
.🏗️ System Architecture
.⚙️ Technical Requirements
.💻 Software Requirements
.📂 Repository Structure
.✨ Features
.▶️ Build Instructions
.🧪 Testing and Demonstration
.📈 Future Enhancements
.👤 Author

📌 Project Overview

This project demonstrates the creation and execution of a Linux daemon process using the C programming language and Linux system calls.

A daemon is a background process that runs independently of direct terminal interaction. It can perform tasks continuously without requiring the user to keep the terminal open.

The project demonstrates the traditional double-fork technique to detach a process from its controlling terminal. It uses system calls such as `fork()`, `setsid()`, `umask()`, and `chdir()` to establish the daemon environment.

The daemon maintains a PID file to identify its process and writes periodic activity messages to a log file. The project helps develop a practical understanding of Linux process management and system programming.

🎯 Objectives

-> Understand daemon processes and background execution in Linux.
-> Create a daemon using the `fork()` system call.
-> Create a new session using `setsid()`.
-> Understand the double-fork daemonization technique.
-> Configure file creation permissions using `umask()`.
-> Change the working directory using `chdir()`.
-> Understand process identification and PID management.
-> Maintain a PID file for identifying the daemon process.
-> Record daemon activity in a log file.
-> Gain practical experience with Linux system calls and C  programming.
   
🔄 Daemon Process Flow

The following diagram illustrates the general daemonization sequence used by this project.

             Program Starts
                   |
                   v
                fork()
                   |
          +--------+--------+
          |                 |
        Parent             Child
          |                 |
         Exit                v
                          setsid()
                             |
                             v
                           fork()
                             |
                   +---------+---------+
                   |                   |
             Intermediate          Final Child
                Parent                 |
                   |                   v
                  Exit          Daemon Initialization
                                       |
                                       v
                                  chdir("/")
                                       |
                                       v
                                   umask(0)
                                       |
                                       v
                              Background Execution
                                       |
                                       v
                               Create PID File
                                       |
                                       v
                              Write Activity Logs
                                       |
                                       v
                               Continue Running

*Note: This is a conceptual flow diagram. The exact sequence should be checked against the implementation in `student_daemon.c.

🏗️ System Architecture
## System Architecture

| S.No. | Component | Description |
|---|---|---|
| 1 | Main Process | Starts the daemon initialization process. |
| 2 | `fork()` | Creates a child process to separate the daemon from the original process. |
| 3 | `setsid()` | Creates a new session and detaches the process from its controlling terminal. |
| 4 | Second `fork()` | Helps ensure the daemon cannot acquire a controlling terminal. |
| 5 | `umask()` | Sets the file permission mask for files created by the daemon. |
| 6 | `chdir()` | Changes the working directory to prevent dependence on the original directory. |
| 7 | PID File | Stores the daemon process ID for identification and monitoring. |
| 8 | Log File | Records daemon activities and status messages. |
| 9 | Background Execution | Allows the daemon to continue running without terminal interaction. |

⚙️ Technical Requirements

## Technical Requirements

| S.No. | Requirement | Description |
|---|---|---|
| 1 | Process Management | Understanding of Linux process creation and termination. |
| 2 | Daemon Process | Knowledge of background processes in Linux. |
| 3 | System Calls | Usage of `fork()`, `setsid()`, `chdir()`, and `umask()`, where implemented. |
| 4 | File Handling | Creating and writing to files for PID storage and logging, where implemented. |
| 5 | Process Monitoring | Checking daemon status and process IDs. |
| 6 | C Programming | Basic knowledge of C programming and system-level programming. |

💻 Software Requirements

| S.No. | Software / Tool | Purpose |
|---|---|---|
| 1 | Linux Operating System | Environment for developing and executing the daemon program. |
| 2 | GCC Compiler | Compiles the C source code. |
| 3 | Terminal | Used to compile, execute, and monitor the daemon. |
| 4 | Text Editor | Used to write and modify the C source code. |
| 5 | Git | Tracks changes in the project source code. |
| 6 | GitHub | Hosts the project repository and documentation. |

📂 Repository Structure

Linux_Daemon-Process/
├── student_daemon.c
├── .gitignore
└── README.md

## Runtime Files

The program uses the following runtime files:

- `/tmp/student_daemon.pid` — stores the daemon's process ID.
- `/tmp/student_daemon.log` — stores periodic daemon activity messages.

These files are generated at runtime and are separate from the source files in the GitHub repository.

✨ Features

* Daemon Creation: Demonstrates Linux daemon process creation in C.
* Double-Fork Technique: Demonstrates process separation during daemonization.
* Session Management:Uses setsid() to establish a new session.
* Background Execution: Runs independently of direct terminal interaction.
* Working Directory Configuration: Uses `chdir("/")` during initialization.
* File Creation Mask:Configures file creation permissions using  umask().
* PID File Management:Records the daemon process ID in /tmp/student_daemon.pid.
* Activity Logging:Writes periodic activity messages to /tmp/student_daemon.log.
* Linux System Programming:Provides practical experience with Linux system calls.

▶️ Build Instructions

1. Open Ubuntu Terminal
Open your Ubuntu terminal.

2. Navigate to the Project Directory
If your source code is located in "~/daemon_project", run:

cd ~/daemon_project

3. Compile the Source Code
Compile the program using GCC:

gcc -Wall -Wextra student_daemon.c -o student_daemon

4. Execute the Program
Run the executable:

./student_daemon

Follow the program's output to observe the daemon initialization process.

5. Verify the Daemon Process
Check whether the process is running:

pgrep -af student_daemon

6. Check the PID File
Display the stored process ID:

cat /tmp/student_daemon.pid

7. Monitor the Log File
View the most recent log entries:

tail -n 10 /tmp/student_daemon.log

*Note: Run the program according to its actual startup behavior. If the daemon is already running, avoid starting duplicate instances.

🧪 Testing and Demonstration

The project can be tested using the following checks:

# Process Verification

Use "pgrep" or "p" to check whether the daemon is running.

pgrep -af student_daemon

# PID Verification

Check whether the PID file contains the process ID.

cat /tmp/student_daemon.pid

# Log Verification

Inspect the log file to confirm that periodic activity messages are being written.

tail -n 10 /tmp/student_daemon.log

# Background Execution Verification

Inspect the process details to examine its process ID, parent process ID, and terminal association.

ps -p "$(cat /tmp/student_daemon.pid)" -o pid,ppid,tty,comm

These checks help demonstrate the daemon's process state and runtime activity.

📈 Future Enhancements

- Implement robust signal handling for graceful termination.
- Improve PID file cleanup when the daemon exits.
- Add duplicate-instance protection using file locking.
- Introduce configurable logging levels and timestamps.
- Improve error handling during daemon initialization.
- Add a systemd service configuration for service management.
- Develop automated tests for process creation and daemon lifecycle management.

👤 Author

**Bhavya Palloli**

GitHub: [bhavyapalloli2004-bit](https://github.com/bhavyapalloli2004-bit)

**Project:** Linux Daemon Process

**Technologies:** C Programming | Linux System Programming | Ubuntu | GCC | Git | GitHub

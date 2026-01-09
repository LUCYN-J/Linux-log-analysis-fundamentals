Linux Log Analysis Fundamentals (Beginner SOC Lab)
📌 Project Objective

This project demonstrates foundational skills in Linux filesystem exploration and basic log analysis from a Security Operations Center (SOC) perspective.

The goal is to understand where logs live, why certain directories matter, and how analysts safely inspect logs before performing deeper investigations.

🖥️ Environment

Operating System: Ubuntu (WSL)

User Type: Standard (non-root)

Tools Used: Linux CLI (ls, less, sudo)

Focus Area: Blue Team / SOC fundamentals

🔍 Step 1: Root Filesystem Orientation
Command Used
ls /

Purpose

Lists the root (/) directory showing the main structure of the Linux operating system.
Before analyzing logs, a SOC analyst must understand how the system is organized.

Observed Directories
bin  boot  dev  etc  home  lib  lib64  media
mnt  opt  proc  root  run  sbin  srv  tmp
usr  var

📂 Security-Relevant Directory Overview
/bin and /sbin

Essential system commands used for normal operation and administration.

/boot

Contains files required to start the system (kernel and bootloader).

/dev

Represents hardware devices (disks, terminals).

/etc ⭐

System configuration files.
Often reviewed to detect unauthorized or malicious configuration changes.

/home ⭐

User home directories.
Common location to find user activity, scripts, or suspicious files.

/proc

Virtual filesystem exposing live process and kernel information.

/sys

Kernel and hardware interface information.

/tmp ⭐

Temporary directory.
Frequently abused by attackers to store payloads or scripts.

/root

Home directory for the root (administrator) user.

/usr

User applications, binaries, and libraries.

/var ⭐⭐⭐

Stores variable data, including logs.
This is the most important directory for SOC investigations.

🔍 Step 2: Log Discovery
Command Used
ls /var/log

Purpose

To identify available logs before opening them.
SOC analysts do not read every log immediately — they first prioritize.

Key Logs Identified

auth.log – Authentication and sudo activity

syslog – General system events

dpkg.log – Package installation and removal history

btmp, wtmp, lastlog – Binary login records

🔍 Step 3: Targeted Log Inspection

After identifying important logs, selected files were inspected safely.

Authentication Logs
sudo less /var/log/auth.log


Used to review:

Successful and failed login attempts

Privilege escalation (sudo) activity

System Logs
less /var/log/syslog


Used to understand:

System events

Service behavior

Errors and warnings

Package Management Logs
less /var/log/dpkg.log


Used to verify:

Software installations

Package updates or removals

Binary Logs (Not Opened Directly)

btmp

wtmp

These logs require specialized commands (last, lastb) and were identified but not directly read.

🧠 Key Learning Outcomes

Understanding Linux filesystem structure is essential before log analysis

/var/log is the primary evidence source during incident response

Analysts prioritize logs instead of opening everything

Text logs and binary logs require different handling

Proper methodology reduces noise and improves investigation efficiency

---
title: Systemd and Python, some Things I Learned
author: Roel M. Hogervorst
date: '2022-07-17'
slug: systemd-and-python-some-things-i-learned
categories:
  - lessons-learned
tags:
  - python
  - systemd
  - linux
  - dagster
---

I have a small computer that I run a python program on. I want to have it run automatically. (the program in question doesn't really matter but it is dagster)

![](/images/wocintech.jpg "three woman with laptops explaining stuff")

Anyway I had some weird issues and because I am sure I will forget this again in the future, here it is for the future:


### python calls a utility in ubuntu but cannot find it
The log says:

```bash
Exception while setting up compute log capture
FileNotFoundError: [Errno 2] No such file or directory: 'tail'
```

This is weird because when I run this command in the terminal it just works.

Cause: systemd does not have access to PATH like other pieces in ubuntu.
But you can add it.  by adding a `Environment=` directive to the service file.

```
Environment="PATH=/usr/bin"
```

### You want to run a program from a virtual environment
Call the shimmed (is that a word?) full path version of the utility or python itself.
If your virtualenv lives in `full-path-to-projectfolder/venv/` make the command `full-path-to-projectfolder/venv/bin/python {command args}`

Or if it is an installed package, the package name: `full-path-to-projectfolder/venv/bin/PACKAGENAME {command args}`

example from me (USERNAME is your username, and venv is where I installed the packages with `python -m venv venv`:

```
ExecStart=/home/USERNAME/dagster_project/venv/bin/dagster-daemon run
Environment="PATH=/home/USERNAME/dagster_project/venv/bin"
```


### you want to run a program from a pyenv environment
Same as above, only the location is somewhere different
`/home/USERNAME/.pyenv/versions/3.9.13/bin`



### example systemd configuration

Has access to .env file, correct working directory and executes the correct python program. 

dagit.service:

```
[Unit]
Description=Dagster dagit service the gui
After=multi-user.target

[Service]
Type=simple
Restart=always
EnvironmentFile=/home/USERNAME/dagster_repo/.env
WorkingDirectory=/home/USERNAME/dagster_repo
ExecStart=/home/USERNAME/.pyenv/versions/3.9.13/bin/dagit -h 0.0.0.0 -p 3000 
Environment="PATH=/home/USERNAME/.pyenv/versions/3.9.13/bin/:/home/USERNAME/.local/bin:/usr/bin"
Environment="DAGSTER_HOME=/opt/dagster/dagster_home"

[Install]
WantedBy=multi-user.target

```


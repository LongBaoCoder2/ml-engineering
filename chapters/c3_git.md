# Git

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Basics of Git](#1-basics-of-git)
  - [1.1. Centralized Version Control](#11-centralized-version-control) 
  - [1.2. Decentralized Cersion Control](#12-decentralized-version-control)
    - [1.2.1. Basics Git Commands](#121-basics-git-commands)
  - [1.3. Branches and Commits](#13-branches-and-commits)
    - [1.3.1. Conflicts in Version Control](#131-conflicts-in-version-control)
    - [1.3.2. Merge a Branch to the Master]()
- [Resources](#resources)


# 1. Basics of Git
## 1.1. Centralized Version Control
- **Limitations of Centralized Version Control**:
  - If the main server goes down, developers can’t save versioned changes
  - Remote commits are slow
  - Unsolicited changes might ruin development
  - If the central database is corrupted, the entire history could be lost (security issues)
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163991997-a63f4f8a-0f39-4b0f-8fab-ff6f2dd5623d.png" width="350" />
</p>

- **Solution**: Decentralized version control
[(Back to top)](#table-of-contents)

## 1.2. Decentralized Version Control
- Local repos host all versions
  - `pull`: get the updates from central server
  - `push`: send the updated repos to the central server
- Advantage:
  - Full history is always available
  - No need to access a remote server (faster access)
  - Abibility to push your changes continously 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163991479-16f40c48-1d3d-4383-9253-51dec9b2e10f.png" width="350" />
</p>

[(Back to top)](#table-of-contents)

### 1.2.1. Basics Git Commands
- `git init`: create a local repo
- `git remote add origin <link_to_remote_server>`: to link the local repo to the remote repo
- `git add <name_of_file>`:  to add a file/files to the stage
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164873696-03b0923b-4f05-488d-9453-899b37647901.png" width="650" />
</p>

- `git commit -m "message"`: to push the commit to the local repo
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164873754-9219d7eb-e292-485b-80d6-f2563d7eb9f8.png" width="450" />
</p>

- `git push -u origin master`: to push the updated files from local repo to remote repo
  - `-u`: to set the upstream as `origin master` 
- `git pull origin <branch_name>`: to pull the latest update from the current branch in the remote server.

[(Back to top)](#table-of-contents)

## 1.3. Branches and Commits
### 1.3.1. Conflicts in Version Control
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163992391-c1c7f0be-8349-4f29-a8a5-6c4a48abac40.png" width="450" />
</p>

### 1.3.2. Merge a branch to the master
- When merging the branch to the master, we need to run a lot of tests. This is very costly.
- **Best Practise**: Try to minimize number of branches, and try to merge the branches to the master as soon as possible.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164874589-8d5f5ee8-0fd4-4bfb-aba9-edcc1bea64f8.png" width="450" />
</p>

## 1.4. Pull Request
- Pull Request: alert to the owner someone wants a change
<p align="center">
  <img width="450" alt="Screenshot 2022-04-23 at 11 57 58" src="https://user-images.githubusercontent.com/64508435/164874357-0e3e6dd7-97b7-4a00-9271-71b318bbfaf4.png">
  <img src="https://user-images.githubusercontent.com/64508435/163994210-70f8cf62-2190-440b-bf34-66533c448cdf.png" width="550" />
</p>

## 1.5. Fork a repo in GitHub
- Once you fork a repo
  - A new repo appears in your account
  - You have complete control over it
  - You can clone the project for local edits
  - Raise a pull request to merge into original repo

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163994488-b02a1d08-1436-4ba8-b7e1-1f4bc79eb49b.png" width="350" />
</p>


[(Back to top)](#table-of-contents)

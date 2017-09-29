===
Git
===


Git is a version control system. When a repository is under git version control, information about all changes made, saved, and commited on any non-ignored file in a repository is saved. This allows you to revert back to previous versions of the repository and search through the history for all commits made to any tracked files in the repository. If you are working with others, using git version control allows you to see every change made to the code, who made it, and why (through the commit messages).

You will need git on your computer to create local git repositories that you can sync with GitHub repositories. Like R, git is open source. You can `download it <https://git-scm.com/downloads>`_ for different operating systems.

After downloading git but before you use it, you should configure it. For example, you should make sure it has your name and email address. You can configure git from a bash shell (for Macs, you can use "Terminal", while for PCs you can use GitBash, which comes with the git installation).

You can use git config functions to configure your version of git. Two changes you should make are to include your name and email address as the user.name and user.email. For example, the following code, if run in a bash shell, would configure a git account for a user named "Jane Doe" who has a generic email address:


.. code-block:: none
    :linenos:
    
    git config --global user.name "Jane Doe"
    git config --global user.email "jane.doe@university.edu"
    
Once you've installed git, you should restart RStudio so RStudio can identify that git is now available. Often, just restarting RStudio will be enough. However, in some cases, you may need to take some more steps to activate git in RStudio. To do this, go to "RStudio" -> "Preferences" -> "Git/SVN". Choose "Enable version control". If RStudio doesn't automatically find your version of git in the "Git executable" box (you'll know it hasn't if that box is blank), browse for your git executable file using the "Browse" button beside that box. If you aren't sure where your git executable is saved, try opening a bash shell and running which git, which should give you the filepath if you have git installed.



Initializing a git repository
*****************************

You can initialize a git repository either using commands from a bash shell or directly from RStudio. First, to initialize a git repository from a bash shell, take the following steps:

- Use a shell ("Terminal" on Macs) to navigate to to that directory. You can use cd to do that (similar to setwd in R).
- Once you are in the directory, first check that it is not already a git repository. To do that, run git status. If you get the message fatal: Not a git repository (or any of the parent directories): .git, it is not yet a git repository. If you do not get an error from git status, the directory is already a repository, so you do not need to initialize it.
- If the directory is not already a git repository, run git init to initialize it as a repository.

For example, if I wanted to make a directory called "example_analysis", which is a direct subdirectory of my home directory, a git repository, I could open a shell and run:

.. code-block:: bash
    :linenos:
    
    cd ~/example_analysis
    git init
    
You can also initialize a directory as a git repository for a directory through R Studio.

- Make the directory an R Project. If the directory is an R package, it likely already has an .Rproj file and so is an R Project. If the directory is not an R Project, you can make it one from RStudio by going to "File" -> "New Project" -> "Existing Directory", and then navigate to the directory you'd like to make an R project.
- Open the R project.
- Go to "Tools" -> "Version Control" -> "Project Setup".
- In the box for "Version control system", choose "Git".

If you do not see "Git" in the box for "Version control system", it means either that you do not have git installed on your computer or that RStudio was unable to find it. If so, see the earlier instructions for making sure that RStudio has identified the git executable.

Once you initialize the project as a git repository, you should have a "Git" window in one of your RStudio panes (top right pane by default). As you make and save changes to files, they will show up in this window for you to commit. For example, below figure is what the Git window for a git repository for writing a coursebook created with bookdown looks like when there are changes to the Week 9 slides that have not yet been commited.

.. image:: https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/6Gzia6XMEea4MxKdJPaTxA_4d86f66fe43265ef4685f2bda623aa6c_ExampleGitWindow.png?expiry=1506729600000&hmac=Bfr7dCnH-ZBpjJrFhj8zcvh6xdRMR3gpoPCHYmSFhGM

Committing
**********

When you want git to record changes, you commit the files with the changes. Each time you commit, you have to include a short commit message with some information about the changes. You can make commits from a shell. However, the easiest workflow for an R project, including R packages, is to make git commits directly from the RStudio environment.

To make a commit from RStudio, click on the "Commit" button in the Git window. That will open a separate commit window that looks like following figure.

.. image:: https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/DU0xLaXNEea4MxKdJPaTxA_9dd0cbf41f5841ac7f95d6cbca75a744_ExampleCommitWindow.png?expiry=1506729600000&hmac=bvM6xOVjkWNnksOhHYR-DDowRSAaT1_iTUsEhGROsPo

In this window, to commit changes:

- Click on the boxes by the filenames in the top left panel to select the files to commit.
- If you'd like, you can use the bottom part of the window to look through the changes you are committing in each file.
- Write a message in the "Commit message" box in the top right panel. Keep the message to one line in this box if you can. If you need to explain more, write a short one-line message, skip a line, and then write a longer explanation.
- Click on the "Commit" button on the right.

Once you commit changes to files, they will disappear from the Git window until you make and save more changes.

Browsing History
****************

On the top left of the Commit window, you can toggle to "History". This window allows you to explore the history of commits for the repository. Below figure shows an example of this window. The top part of this window lists commits to the repository, from most recent to least. The commit message and author are shown for each commit. If you click on a commit, you can use the bottom panel to look through the changes made to that file with a specific commit.

.. image:: https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/NQIjM6XNEeamBAoLccicqA_063fcd4a4ea0adf89c4a824134a55ae6_ExampleHistoryWindow.png?expiry=1506729600000&hmac=WXRcN2eeySBeoKGZeeb1Ulravze-p0qZZSJ27ZUoqiE

==========================
Version Control and GitHub
==========================


Introduction
************


GitHub allows you to post and interact with online code repositories, where all repositories are under git version control. You can post R packages on GitHub and, with the ``install_github`` function from the devtools package, install R packages directly from GitHub. GitHub can be particularly useful for collaborating with others on R packages, as it allows all collaborators to push and pull code between their personal computers and a GitHub repository. While git historically required you to leave R and run git functions at a command line, RStudio now has a number of features that make it easier to interface directly with GitHub.

When using git and GitHub, there are three levels of tasks you'll need to do:

Initial set-up- these are things you will only need to do once (at least per computer)

- Download git
- Configure git with your user name and email
- Set up a GitHub account
- Set up a SSH key to link RStudio on your personal computer with your GitHub account

Set-up of a specific repository- these are things you will need to do every time you create a new repository, but will only need to do once per repository.

- Initialize the directory on your personal computer as a git repository
- Make an initial commit of files in the repository
- Create an empty GitHub repository
- Add the GitHub repository as a remote branch of the local repository
- Push the local repository to the GitHub remote branch
- (If you are starting from a GitHub repository rather than a local repository, either clone the repository or fork and clone the repository instead.)

Day-to-day workflow for a repository- these are things you will do regularly as you develop the code in a repository.

- Commit changes in files in the repository to save git history locally
- Push committed changes to the GitHub remote branch
- Pull the latest version of the GitHub remote branch to incorporate changes from collaborators into the repository code saved on your personal computer
- Write and resolve "Issues" with the code in the repository
- Fix any merge conflicts that come up between different collaborators' code edits
- If the repository is a fork, keep up-to-date with changes in the upstream branch

Each of these elements are described in detail in this section. More generally, this section describes how to use git and GitHub for version control and collaboration when building R packages.

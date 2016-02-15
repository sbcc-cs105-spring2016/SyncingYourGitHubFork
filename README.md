## Syncing Your GitHub Fork

This document describes the process for synchronizing your fork of an assignment to get any changes that have occurred since you forked the repository.

### Why might you need to synchronize

In the course of teaching this course it is possible that I might make mistakes. Sit back for a second think about that statement and then when you recover, continue reading this paragraph. Done? Good. 

It is actually possible, I have made mistakes in the past. And when I do, just your luck I've fixed them after you have already forked the assignment from the SBCC CS105 GitHub site. Now you want those changes so that you can properly finish and submit your assignment for grading. 

For example, let's pretend that in EX03-AlignedNumbers I forgot, or removed, a word from the expected output string of one of the unit tests. No really, that could happen. And then you, being the diligent student that your are tell me about this mistake in the hopes that I will fix it. No really, that could happen too. Then finally, as the conclusion to this preposterous example, I do fix the alleged mistake. The problem is that GitHub is a snapshot system. The fix is in the class repository on the SBCC CS105 GitHub site, but not in your site because that code fix did not exist when you forked the project. So how do we fix this situation?

That's where synchronizing comes into being. The rest of this document will show you how to synchronize your code with the original repository, thus pulling these fixes into your fork. This process can be done either inside Eclipse or on the command line. The Eclipse procedure is the quickest and easiest, but only works in Eclipse. The command line procedure is slightly more complex, but works on any machine where git is installed.

### Before you begin

**NOTE** Please read this section before starting the synchronization process. While you can recover from not following this advice, it can be complex and will probably require my assistance. 

Before you start the synchronization process, be sure to commit and push any changes that are currently in your repository. The synchronization process will try to merge the changes into your repository. If your changes are already in your repository, then git can automatically merge the changes from the original SBCC CS105 GitHub site without any user intervention.

Once you have committed, and **pushed** your changes, you can start the synchronization process below.

### Synchronizing with the forked repository

The process of synchronizing requires 4 steps. The first step is to create a new remote repository. When you first fork and then download a project from your repository, git only knows abou this orignal source. By creating a remote repository you're telling git that your repository also depends on another remote repository, the one you originally forked from. Once you done this, git then nows where to fetch changes from to merge into your repository.

Next, you need to fetch this new remote repository. In order for git to merge your repository with the original it needs to have local copies of both. This step fetches it from the remote repository and places a copy on your local computer.

Next you need to rebase your repository with the remote repository. This step is essentially the merge step. Git takes the remote repository and the replays all the changes you made to your repository on top of this fetched copy. The resulte is your changes are now merged with the corrections made on the original project you forked from.

The final step is to commit and push these changes. As usual with git, your changes are made locally and then you must push them to GitHub in order to make those changes permanent and visible on your GitHub repository.

The following sections will give more detailed instructions on how to perform these steps in Eclipse and in the command line. 

If you wish to see some further discussion of this topic, go to this [StackOverflow article](http://stackoverflow.com/questions/7244321/how-to-update-a-github-forked-repository) where I got the original solution for the command line, or this [EGit documentation page for](http://wiki.eclipse.org/EGit/User_Guide#Adding_a_Remote_Configuration) the original article on how to sync in Eclipse.

#### Synchronizing with Eclipse

The first step in synchronizing with Eclipse is to change to the Git perspective. Perspectives in Eclipse are UI configurations tailored to a specific task. For example, you've been mostly working in the Java perspective for this class. Unfortunately, there's no way to create a new remote repository in the **Team** menu of the Java perspective. Therefore, we need to switch over to the Git perspective.

To change to the Git perspective go to **Window -> Perspective -> Open Perspective** and select **Git** if you've recently opened this perspective, or if you have not select **Other...**.

If you've selected **Other...** you should see something like the following:

![Perspective -> Other...](https://www.dropbox.com/s/yf1qkm7kjhdp27u/perspective-other.png?dl=1) 

Select **Git** and then press **OK**.

You have now changed to the Git perspective. Don't worry, it's only one click in the upper right corner to go back to the Java perspective. The following image shows what the Git perspective looks like, and highlights the Java button you can press to go back to the Java perspective.

![Git Perspective](https://www.dropbox.com/s/w8jc8944yo3rd52/git-perspective.png?dl=1)

#### Synchronizing with the command line

**Note** These commands should be easy to run on Linux or Mac OS X systems. On Windows systems, it might not be quite as straight forward. On Linux and Mac OS X, git is usually already installed. On windows this might not be the case. In the labs, git is installed with Eclipse, and the command line executables may be packaged with that program. With some luck you might be able to find their exact location. If you can't, just follow the directions in 'Synchronizing with Eclipse' in the section above.

Synchronizing on the command line is pretty straight forward and rote. Just issue these commands in the order give. The only piece of information you need to supply the URL to the _original_ repository, **not** your repository. For example, the URL you would need to rebase the EX03-AlignedNumbers project is https://github.com/sbcc-cs105-spring2016/EX03-AlignedNumbers. Once you gotten that URL, execute these commands:

```sh
# Add the remote, call it "upstream":

git remote add upstream https://github.com/sbcc-cs105-spring2016/<Assignment Name>.git

# Fetch all the branches of that remote into remote-tracking branches,
# such as upstream/master:

git fetch upstream

# Make sure that you're on your master branch: This step is optional, and not
# necessary in most situations. It will not hurt anything to run it.

git checkout master

# Rewrite your master branch so that any commits of yours that
# aren't already in upstream/master are replayed on top of that
# other branch:

git rebase upstream/master

# If you want to make this rebase immediately available, force commit the changes

git push -f origin master
```

### After you synchronize



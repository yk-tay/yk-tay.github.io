# Wordpress Git Workflow

## 3:30 PM Thursday, 10 October, 2013
Time to actually [build a website](belavista.md). 

I will check in here whenever there is something new git-related.

----


## 7:18 PM Wednesday, 9 October, 2013
Wrong, those two lines should have been:

```
// define('WP_HOME','http://localhost/clientsite');
// define('WP_SITEURL','http://localhost/clientsite');
```

That makes more sense now.


-----


## 7:03 PM Wednesday, 9 October, 2013
Okay so localhost/clientsite redirected to http://clientsite/wp-admin/install.php which obviously doesnt exist.

Had to comment out two lines in wp-local-config.php to get it to work. I should really find out more about what WP_HOME and WP_SITEURL are.

```
// define('WP_HOME','http://clientsite.com');
// define('WP_SITEURL','http://clientsite.com');
```

----

## 6:52 PM Wednesday, 9 October, 2013
Okay so downloaded wordpress 3.6.1 as a zip file, unzipped into local dev folder, created a new git repo in that folder. (Using SourceTree, and then I had some problem with not being able to commit the current set of files as I had not 'staged' them, so I had to select all the files and add them to the repo, and then committed.

I'm approximately following this, http://roybarber.com/version-controlling-wordpress/, adapted for windows.

Created the local and remote config files, added a .gitignore file.

This is an interesting gitignore file template that doesn't apply to what I'm doing. It excludes core files and only includes the theme files. [https://gist.github.com/jdbartlett/444295]

----

## 5:47 PM Wednesday, 9 October, 2013
Once again Stanley comes to the rescue. I don't actually need to version control core wordpress files.

All I need is:

- The entire client site in a repo, core + theme and plugins
- This repo also on Bitbucket (why?)
- Develop and commit to this repo 
- FTP to client site

----
 

## 5:09 PM Wednesday, 9 October, 2013
Heck, I'm going to go ahead and do a basic setup. I can't afford to delay anymore. A client site awaits!

So let's try this:

- Clone the official wordpress git repo [https://github.com/WordPress/WordPress] into BitBucket. Bitbucket has a nifty importer that does this, keeping all the project history from the github project.
- That went well. 18 branches, 75 tags... Urghh. Do I want this? And I'm pretty sure this isn't tied to the github project (like I can't just sync it with the official repo whenever I want to)
- ???

----


## 4:47 PM Wednesday, 9 October, 2013
So there's a million and one ways/opinion on how to have an integrated git + wordpress development workflow, each with their own pros and cons and requirements. 

[http://stackoverflow.com/questions/6372916/git-workflow-with-wordpress-localhost-to-live]
[http://wordpress.stackexchange.com/questions/85731/wordpress-and-git-workflow?rq=1]
[http://wordpress.stackexchange.com/questions/83046/is-git-github-a-good-wordpress-deployment-solution?rq=1]

There's all these options like branching, submodules...

For example:
> - Got everything with Git setup and installed as far as client goes.
> - Downloaded the latest version of Wordpress in a vanilla install.
> - git init the base install with no modifications
> - Branched the master into "dev" and "live"
> - Work locally, committing in "dev", then once changes are done, merged to live.

#### Workflow involving 2 git repos on the live server

Here's another workflow that requires SSH access on the server, but the neat part about it is that even if one changes a file on the production/live server, it will be pulled into the git repo and tracked.
[http://joemaller.com/990/a-web-focused-git-workflow/] 
[http://danbarber.me/using-git-for-deployment/]. 

#### Workflow involving wordpress core as a subrepository
>  I need to be able to manage my themes and plugins in a git repository, while at the same time keep a reference to the core WordPress files, and allow it to be as easy to update when a new version is released.
[http://davidwinter.me/articles/2012/04/09/install-and-manage-wordpress-with-git/]
[http://wordpress.stackexchange.com/a/100444]
It may require a fix to work properly with some plugins. [http://wordpress.stackexchange.com/questions/107701/development-workflow-for-wordpress-using-git-issues-with-plugins-and-bloginfo]

One can setup wordpress as a submodule within a project, and have that linked to the official wordpress repo, so that changes made on the official core files can be synced into your build. That sounds really convenient and neat. One slight worry would be if there are changes made to core files that 'break' any custom functionality on the site. (Unlikely though.)

I guess I should be realistic and look at how I will actually use this thing. There are two main use cases for me:

1) My own website + an upcoming project - I will have SSH acccess and will be able to use git on the server. This enables a lot of options. These will typically be continually developed, and will benefit the most from version control, the ability to rollback to previous builds, etc. The project will involve a few themes, and then creating a few sites based on each theme (slightly modified). That sounds like each theme should be its own repo, and then branched to create individual sites. 

Actually, no. Each theme should be its own repo, and then each theme will have a child theme that is specific to that site.

2) Client sites on various hosting solutions. - I will only have FTP access. These are typically more bespoke solutions and I think having the whole site (including wordpress core files) in the same repo is the least complicated approach.

----


## 4:51 PM Tuesday, 8 October, 2013
Wow it really took almost an hour. I've got SSH working now, I wish I was more familiar with UNIX shell commands.. I'm sure there's a codeacademy for that.

Thanks to Stanley's handholding, I made it through the SSH configuration and got it up and working. Now I apparently have to setup SSH for Mercurial! Which almost seems unnecessary, it's for something I am unlikely to ever use.

----


## 4:08 PM Tuesday, 8 October, 2013
So now I'm going to set up SSH, which seems geekily neat. My friends at Atlassian seem to be slightly concerned though:

>  setting up an SSH identity can be prone to error. Allow yourself some time, perhaps as much as an hour depending on your experience, to complete this page

Um, okay. Here goes.

----


## 3:37 PM Tuesday, 8 October, 2013
Did another page, this one on playing with the Wiki and Issue Tracker that Bitbucket has. The wiki used to use Creole markup, but Markdown is also an option now. Markdown FTW. I want to use Markdown in everything going forward now. It's so duh. And not being tied to any propritary file format seems nice. 

I think it's part of using computers for so long, you become somewhat jaded about these file formats and lock-in things. Who still has their geocities sites? Blogger (which is still around, I suppose). I used to use a service called Modblog, pretty sure that's defunct. Livejournal has changed management, the list goes on.

----


## 1:27 PM Tuesday, 8 October, 2013
I should stop getting so distracted and get this tutorial over and done with already.

Did another page this morning on adding users, setting permissions, and reviewing the current status of my Bitbucket account, which lets me know if it's time to upgrade to a paying plan.

At the same time, I've realized that, for cases where I have SSH access to my server, I can just use git commands on that server (provided it is installed, if not it shouldn't be hard to install anyway) to pull the latest files from the git repository. 

However, for most client sites, I have only FTP access. This means that whatever I do in git (commits, pushes) will have no impact on the live site until I manually FTP the latest files up to the site. This sucks. If I am modernizing my workflow, I want to be able to do a git commit (maybe with a special flag like DEPLOY) and have it be on the live server automatically.

There are services that can do this such as:
-  [Beanstalk](http://beanstalkapp.com/), which also hosts git repositories, $15usd/mth.
- [Deploy](http://www.deployhq.com/), which links to existing repositories, 6gbp/mth.
- [Ftploy](http://ftploy.com/) which links to Github/Bitbucket, one project is free, ten projects 6gbp/mth

Or, I could look into some workflow where git, or the git software I am using, will flag my FTP software which will run a script to sync a local folder with the remote site.

----


## 5:43 PM Monday, 7 October, 2013
I just finished the mercurial part.. which involved cloning/forking an existing repo, making changes, and creating a pull request.

Thats about it for the day, time to go for a run!

----


## 4:26 PM Monday, 7 October, 2013

Am currently on the 3rd page of the Bitbucket 101, so far I've installed a helper authentication program so I don't have to enter my credentials I upload, created an (empty) repo in the Bitbucket web interface, cloned the blank repo down to a folder on my computer, added a README file, committed that change (git commit), and uploaded it back to BitBucket (git push).

All by using the command line! So spiffy.

----



## 3:41 PM Monday, 7 October, 2013

Signed up for a bitbucket account, wasn't sure if I needed an "individual" account or a "team" account, went with individual.

The initial login page pointed me to this useful Bitbucket 101 guide to getting started, so I'm going through that. [https://confluence.atlassian.com/display/BITBUCKET/Bitbucket+101]. It's meant for both git and mercurial, and estimated to take 60mins or less. I'm hoping less since I'm going to skip the mercurial steps and I have a call at 4:30.

First step is to install Git for windows. I already have it installed, but I figure this is a good chance to update it. I'm pretty sure these fancy modern command-line tools can update themselves from the command line, but couldn't find the command even with a -help, so I went to the page where I was supposed to find the installer. [http://git-scm.com/downloads]. There we find this useful command:

` git clone https://github.com/git/git `

Typed that into my git bash, and it updated itself! (Not before I had to change internet connections, wonky home connection.)

----



## 3:00 PM Monday, 7 October, 2013

So far I've determined that I should use Git, as opposed to SVN or Mercurial or any other versioning software. It seems to be what's most popular now, and I'm sure there are reasons why. No need to research something that's a bit of a 'duh'.

It seems I have a choice between 2 popular hosting solutions, Github and Bitbucket. 

Github seems more for collaboration - You can have unlimited people collaborating on a project, as long as the code is public.

Bitbucket provides unlimited private repos for up to 5 users.

Bitbucket seems more suited for what I want to do, client site development,

----

EOF

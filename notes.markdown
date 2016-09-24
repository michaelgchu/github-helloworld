Activity Log
============
https://guides.github.com/activities/hello-world/

Step 1: Create a Repository
---------------------------
From command-line, did the following:
1. git config --global user.email "my@email.address"
2. mkdir github-helloworld
3. cd github-helloworld
4. .. create a file "README.md" with brief description of this test
5. .. create this file "notes.markdown" to record what I'm doing
6. git init

Step 1b: push to GitHub
-----------------------
Since this is all local, I haven't touched GitHub yet.  Let's try to "force push" it to GitHub using the steps outlined in Rose's post here:
http://stackoverflow.com/questions/17291995/push-existing-project-into-github

As a test, let's try doing this before even creating a repo on GitHub:
1. git status	<-- to confirm the two markdown files are currently untracked
2. git add .	<-- to track them
3. git commit -m "Initial commit"	<-- as it sounds

.. and now, let's see how well this works.  Here are some example project URLs I see:
	https://github.com/d3/d3.git
	https://github.com/JGallardo/urbanhistorical.git
.. so let's assume that a project I could create would/could have a URL like this:
	https://github.com/michaelgchu/githubhelloworld

4. git remote add origin "https://github.com/michaelgchu/githubhelloworld"
5. git remote -v
6. git push origin master

As expected, it failed with error message:
> remote: Repository not found.
> fatal: repository 'https://github.com/michaelgchu/githubhelloworld/' not found

So, must actually create the repo on GitHub now:
7. On GitHub, create new repo with name "github-helloworld" and brief description.
8. Did not choose to initialize with README, since I already have one locally

Done.  The URL is:
> https://github.com/michaelgchu/github-helloworld.git

Oh, and the success webpage also shows commands to push an existing repo:
> git remote add origin https://github.com/michaelgchu/github-helloworld.git
> git push -u origin master

Let's try this now.  Maybe this "git remote add" command will overwrite what I already used?

9. git remote add origin https://github.com/michaelgchu/github-helloworld.git
.. Fail - remote origin already exists.. Ok, so delete first
10. git remote remove origin
11. git remote add origin https://github.com/michaelgchu/github-helloworld.git
12. git remote -v
13. git push -u origin master
.. ERROR!  SSL cert problem:
> $ git push -u origin master
> fatal: unable to access 'https://github.com/michaelgchu/github-helloworld.git/': SSL certificate problem: self signed certificate in certificate chain

GitHub help for "certificate" gives me this:
https://help.github.com/articles/error-ssl-certificate-problem-verify-that-the-ca-cert-is-ok/
Not the same error msg I see, but perhaps its recommended solution will work:
> When you receive this error, it likely means that your CA is out-of-date and needs to be updated. Generally, updating your operating system also updates your CA, and solves the problem.

https://confluence.atlassian.com/bitbucketserverkb/resolving-ssl-self-signed-certificate-errors-806029899.html
This one shows how to temporarily disable SSL check:
> $ GIT_SSL_NO_VERIFY=true git clone https://username@git.example.com/scm/repository.git

http://stackoverflow.com/questions/11621768/how-can-i-make-git-accept-a-self-signed-certificate
Accepted answer's first option mentions permanently accepting a specific certificate

Next steps
* try to update curl?  Does it even have anything re: certs?
* research more... i can't be the only one with this issue
* try to temporarily disable SSL

SUCCESS!  Updated curl to latest version and now on running the same command I get:

$ git push -u origin master --verbose
Pushing to https://github.com/michaelgchu/github-helloworld.git
Username for 'https://github.com':
Password for 'https://michaelgchu@github.com':
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 678 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
POST git-receive-pack (830 bytes)
To https://github.com/michaelgchu/github-helloworld.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
updating local tracking ref 'refs/remotes/origin/master'


Step 1c: push this modified notes file to origin/master
-------------------------------------------------------

Do a final check of things, add this notes file + stuff to staging, commit and then upload/push to origin

1. git status
Oh, I see Vim's .swp file listed.. Let's create a .gitignore file in here that ignores that, plus other things
2. git status
3. git commit -a -m "Update notes; add .gitignore"
4. git push origin master --verbose


# Learn git


## How to delete large binary file from git history

git-filter-repo is a Python script, available at github: https://github.com/newren/git-filter-repo . When installed it looks like a regular git command and can be called by git filter-repo.

You need only one file: the Python3 script git-filter-repo. Copy it to a path that is included in the PATH variable. On Windows you may have to change the first line of the script (refer INSTALL.md). You need Python3 installed installed on your system, but this is not a big deal.

First you can run:
```
git filter-repo --analyze
```
This will generate some statistics files in .git/filter-repo/analysis/ that list that git files by size. This helps you to determine what to do next.

You can delete your DVD-rip file or any other file like this:
```
git filter-repo --invert-paths --path DVD-rip
 ```
Filter-repo is really fast. A task that took around 9 hours on my computer by filter-branch, was completed in 4 minutes by filter-repo. You can do many more nice things with filter-repo. Refer to the documentation for that.

Warning: Do this on a copy of your repository. Many actions of filter-repo cannot be undone. filter-repo will change the commit hashes of all modified commits (of course) and all their descendants down to the last commits!


Removing the remote is by design. Quote from the author:

filter-repo defaults to rewriting the whole repository and as such it creates history incompatible with the original. There are lots of things that can go wrong with pushing a rewritten history back up to the original location, something that other tools did not discuss or warn about in detail and which will trip up many people. Removing the origin remote helps avoid these errors; it is encouragement for folks to stop and read the docs to make sure they are prepared and understand the ramifications (and take appropriate preventative steps) before they do something that may bite them. (They can still push to the remote by just setting it back up, can just re-fetch, etc., so it's easy to circumvent, but I want them to at least notice something is different).

Note it's easy to add the remote back:
```
git remote add <remote_name> <repo-url-here>
```

To push the current branch and set the remote as upstream, use
```
git push --set-upstream <remote_name> main
```


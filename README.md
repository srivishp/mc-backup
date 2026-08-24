# Using Git LFS without storing commit history to reduce repo size
First, download & install Git LFS at
https://git-lfs.com/.

1) Create a local repository and track the required files using ``git lfs track "*.fileExtension"``.
2) Track the gitattributes file using ``git add .gitattributes``.


Follow the steps to update a repo without any commit history or previous records of files.

## Step 1: Add all files
This command stages all the files from your previous history, but only for the purpose of the new commit you are about to create. **Ensure the file keeps the exact same filename every time.**

``git add .``

## Step 2: Overwrite the previous commit
Use the ```--amend``` flag to fuse your new zip file directly into your existing commit. Replace the text in quotes with your custom backup message.

` git commit --amend -m "Commit message"`


## Step 3: Force-push to remote
Overwrite the remote repository with your new, single-commit history.

`git push -f origin master`

If you have other branches that need to be deleted as well, use the `--mirror` flag to force-push everything and erase all remote branches and tags:

`git push -f --mirror origin`

## Step 4: Clean up the ```.git``` folder
Run these three maintenance utility commands in sequence. They instantly delete the old, unreferenced zip versions from your local hard drive rather than waiting Git's default 90-day expiration period.

**Clear the internal undo history diary:**


```git reflog expire --expire=now --all```

**Aggressively delete loose, dangling objects from the core database:**


```git gc --prune=now --aggressive```

**Purge old heavy zip assets from the hidden Git LFS storage cache:**


```git lfs prune```

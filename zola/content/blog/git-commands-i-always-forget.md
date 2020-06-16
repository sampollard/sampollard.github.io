+++
title = "Git Commands I Always Forget"
date = 2020-06-15
description = "Git has some of the most unorthogonal syntax..."
[extra]
category = "Git"
+++
Git has some of the most unorthogonal syntax I've ever used with respect to
branches.  Sometimes, you delineate branches with spaces, sometimes sometimes
you use `/`, sometimes you put flags inbetween the repository and sometimes you
don't. So I just write them down here.

- Pull from a remote branch
  ```
  git checkout --track origin/remotebranch
  ```

- Push to a remote branch
  ```
  git push origin localbranch:remotebranch
  ```

- Delete remote branch
  ```
  git push origin --delete remotebranch
  ```

- Delete a tag remotely
  ```
  git push --delete origin 0.7.0
  ```

- In case you ever mess up and add too many files. Say, you added hundreds of binary files and push,
  so your repository is 10x the size it should be. Even if you remove the folder in the following commit,
  your repo will still have that history. You're rewriting the history books. You can do this with git
  alone, but it's way tougher.
  ```
  git clone --mirror <git URL>
  # Download BFG git cleanup, then run (version number changed, of course)
  java -jar bfg-1.13.0.jar --delete-folders <dirs to delete>
  cd repo.git
  git reflog expire --expire=now --all && git gc --prune=now --aggressive
  # Change so you can push to master on gitlab
  git push
  # IMPORTANT: You want to save the file object-id-map.old-new.txt in the
  # bfg-report so everything gets updated, in say, gitlab. You can find
  # a setting for cleanup under Settings -> Repository -> Cleanup
  ```
  [here](https://docs.gitlab.com/ee/user/project/repository/reducing_the_repo_size_using_git.html)
  is a doc that explains this for Gitlab.


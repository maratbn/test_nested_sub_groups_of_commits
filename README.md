This repo is intended to test doing "groups of commits" as discussed at https://news.ycombinator.com/item?id=27722221 using `git merge --no-ff` as discussed at https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff and is referenced in the question https://stackoverflow.com/questions/68240470/weird-output-from-git-log-graph-when-trying-to-do-nested-sub-groups-of-commi

This repo tests not only groups of commits, but groups of nested sub-groups of commits -- commits for Feature 2A and Feature 2B are intended to be nested sub-groups of the group of commits for Feature 2.

To view the commits grouped together into groups and nested sub-groups it is necessary to view the repo history with `gitk` or do `git log --graph`.


The weird thing is that `git log --graph` produces a weird output when doing "sub-groups":

For example, here is `git log --graph --one-line` of a branch `feature2` that has 2 groups of commits merged in, one group for feature 2A, another group for feature 2B:

```
$ git log --graph --oneline

*   8e4b5f4 (HEAD -> feature2) Merge branch 'feature2b' into feature2
|\  
| * 0ce0350 (feature2b) Feature 2B commit 3.
| * c935021 Feature 2B commit 2.
| * 0bb1c7d Feature 2B commit 1.
|/  
*   58df7c0 Merge branch 'feature2a' into feature2
|\  
| * 682a2ab (feature2a) Feature 2A commit 3.
| * 0f567b0 Feature 2A commit 2.
| * 77a551a Feature 2A commit 1.
|/               (...here the branch was switched to 'feature2'...)
*   1895612 Merge branch 'feature1' (...into 'master'...)
|\  
| * 3809d12 (feature1) Feature 1, 3rd commit.
| * ed91ea8 This is for feature 1, 2nd commit.
| * ffe515d First commit for feature 1.
|/  
* 228a1ab Added 'test1.txt'.
```

But after I `git merge --no-ff feature2` into `master` (to create groups themselves having nested sub-groups) same command produces this weird output:

```
$ git log --graph --oneline

01  *   d6cde88 (HEAD -> master) Merge branch 'feature2'
02  |\  
03  | *   8e4b5f4 (feature2) Merge branch 'feature2b' into feature2
04  | |\  
05  | | * 0ce0350 (feature2b) Feature 2B commit 3.
06  | | * c935021 Feature 2B commit 2.
07  | | * 0bb1c7d Feature 2B commit 1.
08  | |/  
09  | *   58df7c0 Merge branch 'feature2a' into feature2
10  | |\  
11  |/ /  
12  | * 682a2ab (feature2a) Feature 2A commit 3.
13  | * 0f567b0 Feature 2A commit 2.
14  | * 77a551a Feature 2A commit 1.
15  |/               (...here the branch was switched to 'feature2'...)
16  *   1895612 Merge branch 'feature1'
17  |\  
18  | * 3809d12 (feature1) Feature 1, 3rd commit.
19  | * ed91ea8 This is for feature 1, 2nd commit.
20  | * ffe515d First commit for feature 1.
21  |/  
22  * 228a1ab Added 'test1.txt'.
```

Notice how the commit `58df7c0` is displayed as if it is connected to the `master` branch even though it was made in the `feature2` branch, and commits `77a551a` to `682a2ab` are displayed as nested off the `master` branch rather than `feature2`.

Not sure if this is just a bug in `git log --graph`, but right now it is preventing doing groups of nested sub-groups of commits.


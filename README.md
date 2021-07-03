This repo is intended to test doing "groups of commits" as discussed at https://news.ycombinator.com/item?id=27722221 using `git merge --no-ff` as discussed at https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff and is referenced in the question https://stackoverflow.com/questions/68240470/weird-output-from-git-log-graph-when-trying-to-do-nested-sub-groups-of-commi

This repo tests not only groups of commits, but groups of nested sub-groups of commits -- commits for Feature 2A and Feature 2B are intended to be nested sub-groups of the group of commits for Feature 2.

To view the commits grouped together into groups and nested sub-groups it is necessary to view the repo history with `gitk` or do `git log --graph`.


This particular branch uses git "empty commits" to have the desired graph output.  The empty commits have textual description announcing start of work.

For example, here is `git log --graph --one-line` of this branch with the correct output:

```
*   42f1060 (HEAD -> master--w-empty-commits) Merge branch 'feature2--w-empty-commits' into master--w-empty-commits
|\  
| *   26790a3 (feature2--w-empty-commits) Merge branch 'feature2B--w-empty-commits' into feature2--w-empty-commits
| |\  
| | * 9ec4061 (feature2B--w-empty-commits) Feature 2B commit 3.
| | * f7a7543 Feature 2B commit 2.
| | * 9e9b1be Feature 2B commit 1.
| | * 5ca0ef5 Starting work on feature 2B.
| |/  
| *   ef8a461 Merge branch 'feature2A--w-empty-commits' into feature2--w-empty-commits
| |\  
| | * 1a66e4e (feature2A--w-empty-commits) Feature 2A commit 3.
| | * cff6284 Feature 2A commit 2.
| | * 6385f08 Feature 2A commit 1.
| | * 954fb9d Starting work on feature 2A.
| |/  
| * 9319715 Starting work on feature 2.
|/  
*   f036e7c Merge branch 'feature1--w-empty-commits' into master--w-empty-commits
|\  
| * 9e533fb (feature1--w-empty-commits) Feature 1, 3rd commit.
| * b773ce0 This is for feature 1, 2nd commit.
| * 005e310 First commit for feature 1.
| * a408455 Starting work on Feature 1.
|/  
* 228a1ab Added 'test1.txt'.
```



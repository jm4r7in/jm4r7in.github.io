---
published: true
---

## How to fix a local Git repo

1. rename the folder "projects/my-project" to "projects/save-git"
2. Go to the folder "projects/"
3. Run 
	git clone repo-of-my-project
4. Remove all files from "projects/my-project" (except from the folder ".git")
5. Copy all files of "projects/save-git" to "projects/my-project" (except the folder ".git")
6. Go to the folder "projects/my-project"
7. Add the files:
	git add -A
8. Create a commit:
	git commit -m "fixed the f*ck git repo"
9. Push the repo:
	git push origin master



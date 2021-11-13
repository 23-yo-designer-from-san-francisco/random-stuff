[List all the files that ever existed in a Git repository](https://stackoverflow.com/questions/543346/list-all-the-files-that-ever-existed-in-a-git-repository)
[Removing sensitive data from a repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

```bash
git log --pretty=format: --name-only --diff-filter=A | sort -u
```

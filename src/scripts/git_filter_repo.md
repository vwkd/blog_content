# Rewrite history of Git repo using [git-filter-repo](https://github.com/newren/git-filter-repo/)



## Introduction

- allows to change history without changing author date
- can use Python callback function to define flexible logic like exceptions
- can mix and match different callbacks
- prefer to use callback function directly rather than fiddling around with multiple filter arguments
- can think of filter arguments as simple predefined callback function
- just some of capabilities of git-filter-repo, see full [Documentation](https://github.com/newren/git-filter-repo/blob/main/Documentation/git-filter-repo.txt) for everything else it can do



## Remove and/or move files and folders

- exclude path by returning `None`
- rewrite path by returning new path
- beware: if combines with filter arguments can get a `None` filename, can pass through by handling it in first if branch, e.g. `if filename == None: return filename`!
- define callback

```sh
VAR1=$(cat <<EOF
  print("Processing path...", filename)
	// todo: your logic here
	newfilename = filename
  return newfilename
EOF
)
```

- e.g. remove all except subfolder

```sh
VAR1=$(cat <<EOF
  print("Processing path...", filename)
  if filename.startswith(b"foo/bar/baz"):
	  print("Won't change!")
	  return filename
  else:
    return None
EOF
)
```

- e.g. move all into subfolder except one file

```sh
VAR1=$(cat <<EOF
  print("Processing path...", filename)
  if filename == b"README.md":
	  print("Won't change!")
	  return filename
  else:
    return b"src/" + filename
EOF
)
```

- e.g. lowercase path except

```sh
VAR1=$(cat <<EOF
  print("Processing path...", filename)
  if filename == b"README.md":
	  print("Won't change!")
	  return filename
  else:
    return filename.lower()
EOF
)
```

- run command

```sh
git filter-repo --filename-callback $VAR1
```



## Change commit message

- define callback

```sh
VAR2=$(cat <<EOF
  print("Rewriting message", message)
	// todo: your logic here
	newmessage = message
  return newmessage
EOF
)```

- e.g. lowercase all text before a colon

```sh
VAR2=$(cat <<EOF
  print("Rewriting message", message)
  delimiter = b":"
  parts = message.split(delimiter, 1)
  parts[0] = parts[0].lower()
  return delimiter.join(parts)
EOF
)```

- run command

```sh
git filter-repo --message-callback $VAR2
```



## Change author

- run command

```sh
git filter-repo --name-callback 'return name.replace(b"foo", b"bar")' --email-callback 'return email.replace(b"foo", b"bar")'
```



## Move part of repo into new repo

- in first fresh clone of old repo, use git-filter-repo to delete everything except part that wants to move out
- make that the new repo
- in second fresh clone of old repo, use git-filter-repo to delete part that wants to move out
- make that the old repo



## Move part of repo into other repo

- like in [Move part of repo into new repo](#Move_part_of_repo_into_new_repo), but new repo is only temporary
- in other repo, add new repo as remote, fetch, and rebase (or merge), see [StackOverflow](https://stackoverflow.com/questions/1425892/how-do-you-merge-two-git-repositories)

```sh
git remote add new /path/to/new
git fetch new --tags
git rebase new/main main
git remote remove new
```



## Delete branches

- that match regex

```sh
git branch | grep -E "v0\.\d+" | xargs git branch -D
```

- that don't match regex

```sh
git branch | grep -v -E "v0\.\d+" | xargs git branch -D
```


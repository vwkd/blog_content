# Git bulk rename remote



## Introduction

- rename the URL prefix of the given remote of all Git repos in the given directory
- doesn't handle special repos like worktrees, submodules, etc.
- assumes `.git` directory is from Git, doesn't descend into it



## Usage

```sh
./script.sh my_repos foo@bar.com foo@baz.com origin
./script.sh my_repos https://foo.com/ https://bar.com/ origin
```



## Script


```sh
#!/usr/bin/env bash

set -euo pipefail

if [ $# -ne 4 ]; then
  echo "usage: $0 ROOT_DIR OLD_PREFIX NEW_PREFIX REMOTE_NAME" >&2
  exit 1
fi

ROOT=$1
OLD=$2
NEW=$3
REMOTE=$4

if [ ! -d "$ROOT" ]; then
  echo "error: '$ROOT' is not a directory" >&2
  exit 1
fi

if [ -z "$OLD" ] || [ -z "$NEW" ]; then
  echo "error: OLD_PREFIX and NEW_PREFIX must be non-empty" >&2
  exit 1
fi

if [ "$OLD" = "$NEW" ]; then
  echo "error: OLD_PREFIX and NEW_PREFIX must differ" >&2
  exit 1
fi

find "$ROOT" -type d -name .git -prune -print | while IFS= read -r gitdir; do
  repo=${gitdir%/.git}

  if ! git -C "$repo" rev-parse --is-inside-work-tree >/dev/null 2>&1; then
    continue
  fi

  url=$(git -C "$repo" remote get-url "$REMOTE" 2>/dev/null || true)

  if [ -z "$url" ]; then
    continue
  fi

  case "$url" in
    "$OLD"*)
      suffix=${url#"$OLD"}
      new_url="$NEW$suffix"
      if git -C "$repo" remote set-url "$REMOTE" "$new_url" >/dev/null 2>&1; then
        echo "$repo"
      else
        echo "failed to update $repo" >&2
      fi
      ;;
    *)
      # noop
      :
      ;;
  esac
done
```

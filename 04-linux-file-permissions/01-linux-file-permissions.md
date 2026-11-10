# Linux File Permissions

I checked the file and directory permissions in a research team's project folder on Linux, found the ones that gave too much access, and fixed them with `chmod`.

## Scenario

I am a security professional working with a research team. My task is to check the file permissions in `/home/researcher2/projects` (user `researcher2`, group `research_team`) and make sure they match the authorization that should be given, removing any unauthorized access.

## Skills used

| Area | Used for |
|---|---|
| Linux command line | Moving between directories (`pwd`, `cd`) |
| `ls -l` / `ls -la` | Listing files with their permissions, including hidden files |
| Reading permission strings | Finding who can read, write or execute each file |
| `chmod` | Removing or adding permissions |
| Least privilege | Giving each user and group only the access they need |

## Starting permissions

```
$ pwd
/home/researcher2
$ cd projects/
$ ls -la
drwxr-xr-x 3 researcher2 research_team 4096 Nov 9 10:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Nov 9 10:18 ..
-rw--w---- 1 researcher2 research_team   46 Nov 9 10:13 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Nov 9 10:13 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Nov 9 10:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Nov 9 10:13 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Nov 9 10:13 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Nov 9 10:13 project_t.txt
```

### How to read a permission string

Example: `-rw-rw-r--` (project_r.txt)

| Position | Characters | Meaning |
|---|---|---|
| 1 | `-` | Type: `-` = file, `d` = directory |
| 2–4 | `rw-` | User (owner): read, write, no execute |
| 5–7 | `rw-` | Group: read, write, no execute |
| 8–10 | `r--` | Other: read only |

`r` = read, `w` = write, `x` = execute, `-` = no permission.

## Changes made

| File / directory | Before | Command | After | Why |
|---|---|---|---|---|
| `project_k.txt` | `-rw-rw-rw-` | `chmod o-w project_k.txt` | `-rw-rw-r--` | Other should not have write access to any file |
| `project_m.txt` | `-rw-r-----` | `chmod g-r project_m.txt` | `-rw-------` | The group should not read this file |
| `.project_x.txt` (hidden) | `-rw--w----` | `chmod u-w,g-w,g+r .project_x.txt` | `-r--r-----` | User and group can read it, but no one can write to it |
| `drafts/` | `drwx--x---` | `chmod g-x drafts/` | `drwx------` | Only `researcher2` should access this directory |

`project_r.txt` and `project_t.txt` were already correct, so I did not change them.

### chmod in short

| Part | Meaning |
|---|---|
| `u` / `g` / `o` | User / group / other |
| `-` / `+` | Remove / add a permission |
| `r` / `w` / `x` | Read / write / execute |

Example: `chmod o-w project_k.txt` = remove write permission from other.

## Report

### Project description
In this project we're working on permissions on the files in the `/home/researcher2/projects` directory for the `researcher2` user. `researcher2` is a part of the `research_team` group. In this activity we're checking the correct authorization for the user and group. We're checking the necessary permissions for all the files and directories, including the hidden files, and making sure that permissions align with the authorization that should be given.

### Check file and directory details
I checked the permissions of the projects directory and the files it contains. I used `ls -l` (long list), which lists the files and directories in a detailed manner. I also used `ls -la`, where `-a` lists all files including hidden files and directories.

### Describe the permissions string
If the string starts with `d` it's a directory, and if it starts with `-` it's a file. Characters 2–4 are for the user, 5–7 for the group and 8–10 for other, followed by read, write and execute permissions, and `-` means there's no permission. Hidden files have a dot (`.`) prefix, for example `.project_x.txt`.

- `project_k.txt`: user rw, group rw, other rw
- `project_m.txt`: user rw, group r, other none
- `project_r.txt`: user rw, group rw, other r
- `project_t.txt`: user rw, group rw, other r
- `.project_x.txt`: user rw, group w, other none

### Change file permissions
I determined whether any files had incorrect permissions and changed them as needed, to remove unauthorized access and strengthen security. `chmod o-w` is used to modify the permission, where u = user, g = group and o = other, and `-` removes a permission. `o-w` means removing write permission from other, because other should not have write access to any file. I ran `chmod g-r project_m.txt` to remove read permission for the group on `project_m.txt`.

### Change file permissions on a hidden file
I changed the permissions of the hidden file `.project_x.txt` so that both the user and the group can read, but not write to, the file, using `chmod u-w,g-w,g+r .project_x.txt`.

### Change directory permissions
The group had execute permission only on the `drafts` directory. Only the `researcher2` user should be allowed to access the `drafts` directory and its contents, so I used `chmod g-x drafts/`.

### Summary
In this activity I practiced managing different levels of authorization on files and directories. First I used `pwd` to check the present working directory, which makes navigation easier. Then I used `ls -l` to list the files and directories in the projects directory and `ls -la` to also list the hidden files. Then I changed the necessary read, write and execute permissions for user, group and other using the `chmod` command. Now the permissions match the authorization the organization wants, and unauthorized access is removed.

## What I learned

- Always use `ls -la`, not only `ls -l`, so hidden files are checked too.
- "Other" should almost never have write access.
- `chmod` can change several permissions in one command, separated by commas.

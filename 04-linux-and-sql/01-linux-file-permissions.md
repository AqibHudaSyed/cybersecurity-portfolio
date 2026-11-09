Course 4 (Tools of the Trade: Linux and SQL) portfolio activity — "Use Linux commands to manage file permissions". Reviewed in Course 4 chat, final 8/8. Please make the portfolio .md.

TARGET: new folder 04-linux-and-sql/ with index README.md (same style as Course 3 folder) + 01-linux-file-permissions.md; add row 04 in main README. No mistakes section. Report section = my final text below (light grammar fixes only, keep my wording).

SCENARIO (own words): I am a security professional working with a research team. My task is to check the file permissions in /home/researcher2/projects (user researcher2, group research_team) and make sure they match the authorization that should be given, removing any unauthorized access.

LOGS:
$ pwd → /home/researcher2
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

Changes:
chmod o-w project_k.txt              → -rw-rw-r--
chmod g-r project_m.txt              → -rw-------
chmod u-w,g-w,g+r .project_x.txt     → -r--r-----
chmod g-x drafts/                    → drwx------

MY FINAL REPORT:
Project description: In this project we're working on permissions on the files in the /home/researcher2/projects directory for the researcher2 user. researcher2 is a part of the research_team group. In this activity we're checking the correct authorization for the user and group. We're checking the necessary permissions for all the files and directories, including the hidden files, and making sure that permissions align with the authorization that should be given.

Check file and directory details: I checked the permissions of the projects directory and the files it contains. I used ls -l (long list), which lists the files and directories in a detailed manner. I also used ls -la, where "-a" lists all files including hidden files and directories.

Describe the permissions string: If the string starts with "d" it's a directory, and if it starts with "-" it's a file. Characters 2-4 are for the user, 5-7 for the group and 8-10 for other, followed by read, write and execute permissions, and "-" means there's no permission. Hidden files have a dot (.) prefix, for example .project_x.txt. (Plus my per-file list: project_k = u rw / g rw / o rw; project_m = u rw / g r / o none; project_r = u rw / g rw / o r; project_t = u rw / g rw / o r; .project_x = u rw / g w / o none.)

Change file permissions: I determined whether any files had incorrect permissions and changed them as needed, to remove unauthorized access and strengthen security. chmod o-w is used to modify the permission, where u=user, g=group and o=other, and "-" removes a permission. "o-w" means removing write permission from other, because other should not have write access to any file. I ran chmod g-r project_m.txt to remove read permission for the group on project_m.txt.

Change file permissions on a hidden file: I changed the permissions of the hidden file .project_x.txt so that both the user and the group can read, but not write to, the file, using chmod u-w,g-w,g+r .project_x.txt.

Change directory permissions: The group had execute permission only on the drafts directory. Only the researcher2 user should be allowed to access the drafts directory and its contents, so I used chmod g-x drafts/.

Summary: In this activity I practiced managing different levels of authorization on files and directories. First I used pwd to check the present working directory, which makes navigation easier. Then I used ls -l to list the files and directories in the projects directory and ls -la to also list the hidden files. Then I changed the necessary read, write and execute permissions for user, group and other using the chmod command. Now the permissions match the authorization the organization wants, and unauthorized access is removed.

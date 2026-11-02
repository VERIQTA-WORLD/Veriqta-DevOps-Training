# Day 02 notes

## 1. The filesystem is your application's filing system

Imagine a restaurant with separate places for recipes, supplies, and order slips. A recipe does not belong in the waste bin, and copying a recipe is different from moving the only original. Your application's configuration, documentation, logs, releases, and backups also need distinct purposes.

Directories organize names. Files contain data. A correct-looking filename does not prove correct content. A directory called backups does not prove that a backup is usable.

![The purpose of each directory in a learning-platform workspace.](../07%20Images/workspace.svg)

Text equivalent: config holds synthetic configuration, docs holds operating instructions, logs is reserved for later service logs, backups holds reviewed before-change copies, and scratch holds explicitly disposable practice files.

Every command example below is copyable. Run one block at a time in the stated directory. Expected output is illustrative unless an exact file value is specified. Do not paste output blocks into the shell.

## 2. Check identity and create a private practice area

Confirm that the comparison and inventory utilities are available before changing files:

```bash
cmp --version
```

Expected: a version banner identifying GNU Diffutils. This reads tool information and changes no files.

```bash
find --version
```

Expected: a version banner identifying GNU Findutils. Your installed version may differ from another learner's. If either command is missing or a different implementation rejects an option, stop and establish distribution-appropriate setup before using the dependent exercise. Do not guess an installation command for an unknown distribution.

```bash
id -u
```

Expected: a nonzero numeric ID. If it is zero, use an existing authorized regular account. No administrator command is required today.

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-02/notes-practice"
```

Expected: no output. The option creates missing parents and accepts existing directories without emptying them. This changes your filesystem only under your lab home path. On a repeat visit, inspect existing work rather than replacing it blindly.

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/notes-practice"
```

Expected: normally no output. Verify your location:

```bash
pwd
```

Expected path ending:

```text
/veriqta-devops-labs/linux/day-02/notes-practice
```

Your home prefix differs between users. Check it before changing files.

## 3. Absolute, relative, current, and parent paths

An absolute path starts at the filesystem root. A relative path starts from your working directory. A dot means the current directory; two dots mean its parent. Your home variable already exists; do not reassign it.

Create a child directory:

```bash
mkdir records
```

Expected: no output on a fresh run. If it already exists, inspect it and continue only if it is your practice directory.

Enter it using a relative path:

```bash
cd records
```

Expected: no output. Verify:

```bash
pwd
```

Expected: the notes-practice path followed by `/records`.

Return to the parent:

```bash
cd ..
```

Expected: no output. Check again:

```bash
pwd
```

Expected: notes-practice, without `/records` at the end. You changed location; you did not delete records.

An absolute home-based path works from any current directory:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/notes-practice"
```

Expected: no output. Relative filenames used next are interpreted from this directory.

## 4. Names, spaces, and leading hyphens

Linux names are generally case-sensitive. The names Config and config can refer to different directories. Hidden entries begin with a dot. Hidden does not mean encrypted, protected, or safe to publish.

Create a directory whose name includes a space:

```bash
mkdir "draft notes"
```

Expected: one directory named draft notes. Quotes group the name into one argument; quote characters do not become part of it.

Inspect the directory itself:

```bash
ls -ld -- "draft notes"
```

Expected: one metadata line beginning with a directory indicator. The long-listing option includes metadata; the directory option inspects the named directory rather than its children. The double hyphen ends option parsing. Here it is a defensive separator, not part of the filename.

Avoid wildcard deletion in this lesson. A wildcard can select more files than you intended, and its expansion is a separate shell behavior you will study later.

## 5. Create an empty marker and inspect hidden entries

```bash
touch -- .lab-marker
```

Expected: no output. This creates an empty file if absent. If the file already exists, it updates its timestamps; it does not empty existing content. An empty marker is not a populated configuration file.

```bash
ls -l
```

Expected: a long listing of ordinary entries, including records and draft notes. A default listing does not show the hidden marker.

```bash
ls -la
```

Expected: the marker is now visible, along with dot entries representing the current and parent directories. The additional option includes hidden entries. Listing order and metadata can vary.

## 6. Write a small source file

```bash
vi records/source.txt
```

Expected: vi opens the file. On a fresh run, press i and type:

```text
platform=learning
release=v001
```

Press Esc, then enter this **inside vi** and press Enter:

```text
:wq
```

Expected: saved file and return to the shell. If the file already exists, inspect it before editing. Read what was saved:

```bash
cat records/source.txt
```

Expected exact content:

```text
platform=learning
release=v001
```

The slash in the filename selects a child directory. It does not create that directory automatically.

## 7. Copy without discarding the source

```bash
cp -i -- records/source.txt records/copy.txt
```

Expected on a fresh run: no output, and both files exist. The interactive option asks before overwriting an existing destination. An unexpected overwrite prompt means stop and inspect the destination. Answer n and press Enter if you do not intend replacement.

Inspect both files:

```bash
ls -l -- records/source.txt records/copy.txt
```

Expected: two regular-file listings. That proves two names exist, not that their contents match.

Compare the bytes:

```bash
cmp -- records/source.txt records/copy.txt
```

Expected for identical files: no output. Immediately check the comparison status:

```bash
echo $?
```

Expected:

```text
0
```

The shell stores the last command's exit status in a special value, and echo displays it. Read it immediately; another command replaces it. For this comparison utility, zero means equal, one means different, and a value greater than one means trouble such as a missing input. This small check is enough for today's verification; shell control flow comes later.

The comparison checks content, not ownership, permissions, or recovery durability.

## 8. Rename or move deliberately

Rename the copy:

```bash
mv -i -- records/copy.txt records/reviewed.txt
```

Expected: no output if the destination is absent. The old copy name is replaced by the reviewed name. The original source file remains. The interactive option asks before overwriting an existing destination.

Inspect the parent directory:

```bash
ls -l -- records
```

Expected: source.txt and reviewed.txt. A move can also change directories. It is not a backup because the old source name is removed after a successful move.

## 9. Copy a small directory

Only do this if snapshot does not already exist in notes-practice. Check first:

```bash
ls -ld -- snapshot
```

Expected on a fresh run: an error indicating that snapshot does not exist. This inspection is an intentional absence check. If it exists, do not repeat the copy into it; inspect or choose a new snapshot name instead.

```bash
cp -Ri -- records snapshot
```

Expected: no output and a new snapshot directory containing the two files. The recursive option copies directory contents. The interactive option protects existing destination files from unexamined replacement.

```bash
ls -la -- snapshot
```

Expected: source.txt and reviewed.txt. Copying to a destination directory that already exists can create an extra nested source directory. Establish whether the destination exists before choosing the command. A recursive copy is not a complete backup policy for a running database or production system.

## 10. Inspect a bounded directory tree

```bash
find . -maxdepth 2 -print
```

Expected: relative paths beginning with the current directory, with descendants at most two levels below it. The dot is the starting point, the depth option limits traversal, and the final action prints each path. Order is not guaranteed. Hidden entries can appear.

This is a read-only inventory. Do not add a deletion action to the command.

## 11. Remove only an approved disposable file

Create a file specifically for this removal exercise:

```bash
touch -- disposable.txt
```

Expected: no output. Inspect the exact target:

```bash
ls -l -- disposable.txt
```

Expected: a regular-file listing. Confirm you are in notes-practice and the file is only the disposable exercise file.

```bash
rm -i -- disposable.txt
```

Expected: a prompt asking whether to remove that file. Type y and press Enter only after checking the name. This removes the file directly; there is no guaranteed desktop recycle-bin recovery.

Verify absence:

```bash
ls -l -- disposable.txt
```

Expected: a file-not-found error. This expected error is the verification result, not a reason to recreate the deleted file.

Remove the empty directory created earlier:

```bash
rmdir -- "draft notes"
```

Expected: no output if it is empty. If it reports that the directory is not empty, inspect its contents, including hidden files. Do not escalate to recursive deletion. Your records and snapshot should remain intact.

## 12. Engineering habits

Check location before mutation. Inspect both source and destination. Preserve a verified before-change copy. Compare content after copying and restoring. Record unexpected prompts and exact errors. An unchanged filename does not prove unchanged content, and a successful command is not a complete operational test.

## Official references

- [GNU copy behavior](https://www.gnu.org/software/coreutils/manual/html_node/cp-invocation.html).
- [GNU move behavior](https://www.gnu.org/software/coreutils/manual/html_node/mv-invocation.html).
- [GNU file removal](https://www.gnu.org/software/coreutils/manual/html_node/rm-invocation.html).
- [GNU empty-directory removal](https://www.gnu.org/software/coreutils/manual/html_node/rmdir-invocation.html).
- [GNU comparison utility](https://www.gnu.org/software/diffutils/manual/html_node/Invoking-cmp.html).
- [GNU traversal depth](https://www.gnu.org/software/findutils/manual/html_node/find_html/Directories.html).
- [GNU Coreutils reference](https://www.gnu.org/software/coreutils/manual/coreutils.html), identity, listing, directory creation, timestamps, and reading.

[Follow Along Lab](../02%20Follow%20Along%20Lab/README.md) · [Day 02](../README.md)

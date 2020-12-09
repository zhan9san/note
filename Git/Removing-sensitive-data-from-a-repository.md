# Removing sensitive data from a repository

Reference:  
`https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository`

1. If you don't already have a local copy of your repository with sensitive data in its history, clone the repository to your local computer.

    ```Bash
    git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
    > Initialized empty Git repository in /Users/YOUR-FILE-PATH/YOUR-REPOSITORY/.git/
    > remote: Counting objects: 1301, done.
    > remote: Compressing objects: 100% (769/769), done.
    > remote: Total 1301 (delta 724), reused 910 (delta 522)
    > Receiving objects: 100% (1301/1301), 164.39 KiB, done.
    > Resolving deltas: 100% (724/724), done.
    ```

2. Navigate into the repository's working directory.

   ```Bash
   $ cd YOUR-REPOSITORY
   >Show nothing
   ```

3. Run the following command, replacing `PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA` with the path to the file you want to remove, not just its filename. These arguments will:
   * Force Git to process, but not check out, the entire history of every branch and tag
   * Remove the specified file, as well as any empty commits generated as a result
   * **Overwrite your existing tags**

    ```Bash
    $ git filter-branch --force --index-filter \
    "git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA" \
    --prune-empty --tag-name-filter cat -- --all
    > Rewrite 48dc599c80e20527ed902928085e7861e6b3cbe6 (266/266)
    > Ref 'refs/heads/main' was rewritten
    ```

    **Note**: If the file with sensitive data used to exist at any other paths (because it was moved or renamed), you must run this command on those paths, as well.

4. Add your file with sensitive data to `.gitignore` to ensure that you don't accidentally commit it again.

    ```Bash
    $ echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
    $ git add .gitignore
    $ git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
    > [main 051452f] Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore
    >  1 files changed, 1 insertions(+), 0 deletions(-)
    ```

5. Double-check that you've removed everything you wanted to from your repository's history, and that all of your branches are checked out.
6. Once you're happy with the state of your repository, force-push your local changes to overwrite your GitHub repository, as well as all the branches you've pushed up:

    ```Bash
    $ git push origin --force --all
    > Counting objects: 1074, done.
    > Delta compression using 2 threads.
    > Compressing objects: 100% (677/677), done.
    > Writing objects: 100% (1058/1058), 148.85 KiB, done.
    > Total 1058 (delta 590), reused 602 (delta 378)
    > To https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
    >  + 48dc599...051452f main -> main (forced update)
    ```

7. In order to remove the sensitive file from your tagged releases, you'll also need to force-push against your Git tags:
    ```Bash
    $ git push origin --force --tags
    > Counting objects: 321, done.
    > Delta compression using up to 8 threads.
    > Compressing objects: 100% (166/166), done.
    > Writing objects: 100% (321/321), 331.74 KiB | 0 bytes/s, done.
    > Total 321 (delta 124), reused 269 (delta 108)
    > To https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
    >  + 48dc599...051452f main -> main (forced update)
    ```

8. Contact GitHub Support or GitHub Premium Support, asking them to remove cached views and references to the sensitive data in pull requests on GitHub.

9. Tell your collaborators to rebase, not merge, any branches they created off of your old (tainted) repository history. One merge commit could reintroduce some or all of the tainted history that you just went to the trouble of purging.

10. After some time has passed and you're confident that git filter-branch had no unintended side effects, you can force all objects in your local repository to be dereferenced and garbage collected with the following commands (using Git 1.8.5 or newer):

    ```Bash
    $ git for-each-ref --format="delete %(refname)" refs/original | git update-ref --stdin
    $ git reflog expire --expire=now --all
    $ git gc --prune=now
    > Counting objects: 2437, done.
    > Delta compression using up to 4 threads.
    > Compressing objects: 100% (1378/1378), done.
    > Writing objects: 100% (2437/2437), done.
    > Total 2437 (delta 1461), reused 1802 (delta 1048)
    ```

    **Note**: You can also achieve this by pushing your filtered history to a new or empty repository and then making a fresh clone from GitHub.

Reference: `https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository`

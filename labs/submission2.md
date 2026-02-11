```bash
1) git log --oneline -1

8c2a010 (HEAD -> feature/lab2) Add more content
 
2) git cat-file -p 8c2a010
tree 23e91942ff3ce7ef439dcdeba8c75173cf395326
parent 7870170b70e1e9acb13bf0c1c0375d0d926c0ea1
author Aliya Latipova <aliyalatipova@gmail.com> 1770640763 +0300
committer Aliya Latipova <aliyalatipova@gmail.com> 1770640763 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgahbMKjqXpbDKS/yq0XmYOEr+XA
 gJ5eIIRzF+OYwLaM4AAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQM34P0pE74XTF5hqymDmlRik9liI3U48nNiXoigp1TT5VOPoXyBEcF1oLuO0hJ/XlP
 iAPGSegPs5to209pQGEAU=
 -----END SSH SIGNATURE-----

3)  git cat-file -p 23e91942ff3ce7ef439dcdeba8c75173cf395326

040000 tree 4b00f342961d74262fbb50ff469745d0fc7ea83a    .github
040000 tree 49ea7b4ab1503744ae47d10ae33ea487c3c93d37    .idea
100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb    README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
040000 tree 25aa0d3a77eaf13b24ceb49e72e0de5a84dd78b5    labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
100644 blob e002b84b36d7cda3ed4accb7cf0d28546c2057d0    test.txt
100644 blob 29a6b9da669445d31f6dd05f14318ea39aa6ecd1    test_signed_commit.txt
100644 blob 5c02253e4d038dbb3a20c2f6b9fa4d4b567aeb3f    verification_test.md

4)  git cat-file -p e002b84b36d7cda3ed4accb7cf0d28546c2057d0
��Test content
More content

5)  git cat-file -t 8c2a010
commit
```

типы  объектов:
Blob — хранит содержимое файлов (например, текст test.txt)

Tree — хранит структуру каталогов (какие файлы и папки есть, их права доступа и хэши)

Commit — хранит снимок состояния: ссылку на дерево, родительский коммит, автора, время и сообщение


Git хранит данные как неизменяемые объекты с уникальными SHA-1 хэшами. Каждый коммит ссылается на дерево, которое ссылается на blobs и другие деревья. Если файл изменяется, создается новый blob, и дерево обновляется с новым хэшем.




## таск 2
```bash
1)  git log --oneline -3
c5e8d1f (HEAD -> git-reset-practice) Third commit
7831243 Second commit
9693ba7 First commit
2)  cat file.txt
First commit
Second commit
Third commit

3) git reset --soft HEAD~1
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git log --oneline -2
7831243 (HEAD -> git-reset-practice) Second commit
9693ba7 First commit

4) cat file.txt
First commit
Second commit
Third commit

5)  git reflog
7831243 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
c5e8d1f HEAD@{1}: commit: Third commit
7831243 (HEAD -> git-reset-practice) HEAD@{2}: commit: Second commit
9693ba7 HEAD@{3}: commit: First commit
8c2a010 (feature/lab2) HEAD@{4}: checkout: moving from feature/lab2 to git-reset-practice
8c2a010 (feature/lab2) HEAD@{5}: checkout: moving from git-reset-practice to feature/lab2
a909129 HEAD@{6}: reset: moving to HEAD~1
f53175a HEAD@{7}: reset: moving to HEAD~1
6428fca HEAD@{8}: commit: Reset practice: Third commit
f53175a HEAD@{9}: commit: Reset practice: Second commit
a909129 HEAD@{10}: commit: Reset practice: First commit
8c2a010 (feature/lab2) HEAD@{11}: checkout: moving from feature/lab2 to git-reset-practice
8c2a010 (feature/lab2) HEAD@{12}: commit: Add more content
7870170 HEAD@{13}: commit: Add test file
f8a853d (origin/feature/lab1, feature/lab1) HEAD@{14}: checkout: moving from feature/lab1 to feature/lab2
:


6) git reset --hard c5e8d1f
HEAD is now at c5e8d1f Third commit

7)  git log --oneline -3
c5e8d1f (HEAD -> git-reset-practice) Third commit
7831243 Second commit
9693ba7 First commit

8)  git reset --hard HEAD~1
HEAD is now at 7831243 Second commit
9) PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git log --oneline -2
7831243 (HEAD -> git-reset-practice) Second commit
9693ba7 First commit
10) PS C:\Users\aliya\PycharmProjects\DevOps-Intro> cat file.txt
First commit
Second commit

11) git reflog
7831243 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
c5e8d1f HEAD@{1}: reset: moving to c5e8d1f
7831243 (HEAD -> git-reset-practice) HEAD@{2}: reset: moving to HEAD~1
c5e8d1f HEAD@{3}: commit: Third commit
7831243 (HEAD -> git-reset-practice) HEAD@{4}: commit: Second commit
9693ba7 HEAD@{5}: commit: First commit
8c2a010 (feature/lab2) HEAD@{6}: checkout: moving from feature/lab2 to git-reset-practice
8c2a010 (feature/lab2) HEAD@{7}: checkout: moving from git-reset-practice to feature/lab2
a909129 HEAD@{8}: reset: moving to HEAD~1
f53175a HEAD@{9}: reset: moving to HEAD~1
6428fca HEAD@{10}: commit: Reset practice: Third commit
f53175a HEAD@{11}: commit: Reset practice: Second commit
a909129 HEAD@{12}: commit: Reset practice: First commit
8c2a010 (feature/lab2) HEAD@{13}: checkout: moving from feature/lab2 to git-reset-practice
8c2a010 (feature/lab2) HEAD@{14}: commit: Add more content
:
12) git reset --hard c5e8d1f
HEAD is now at c5e8d1f Third commit

13) git log --oneline -3
c5e8d1f (HEAD -> git-reset-practice) Third commit
7831243 Second commit
```

### таск 3
```bash
git log --oneline --graph --all --decorate
* 82e4d35 (side-branch) Side branch commit
| * c5e8d1f (git-reset-practice) Third commit
| * 7831243 Second commit
| * 9693ba7 First commit
|/
* 8c2a010 (HEAD -> feature/lab2) Add more content
* 7870170 Add test file
* f8a853d (origin/feature/lab1, feature/lab1) docs: fixed lab1 submission
* 3afcdcf docs: add commit signing summary
* a1501fc docs: add signed commit for verification
* 742f0e6 (origin/main, origin/HEAD, main) feat: add PR template
* a7b704e test: verify commit signing
:...skipping...
* 82e4d35 (side-branch) Side branch commit
| * c5e8d1f (git-reset-practice) Third commit
| * 7831243 Second commit
| * 9693ba7 First commit
|/
* 8c2a010 (HEAD -> feature/lab2) Add more content
* 7870170 Add test file
* f8a853d (origin/feature/lab1, feature/lab1) docs: fixed lab1 submission
* 3afcdcf docs: add commit signing summary
* a1501fc docs: add signed commit for verification
* 742f0e6 (origin/main, origin/HEAD, main) feat: add PR template
* a7b704e test: verify commit signing
* 5a438cb docs: add lab1 submission
* 0c15da0 docs: add commit signing summary
* d6b6a03 Update lab2
* 87810a0 feat: remove old Exam Exemption Policy
| * 0a09c16 (origin/release/f25) feat: remove old Exam Exemption Policy
|/
* 1e1c32b feat: update structure
* 6c27ee7 feat: publish lecs 9 & 10
:
```

## Task 4 — Tagging Commits

### Создание и отправка тегов
```bash
# Создание тега v1.0.0 на текущем коммите
git tag v1.0.0

# Отправка тега на удаленный репозиторий
git push origin v1.0.0
```

### таск 5
```bash
# Создай новую ветку и переключись на неё
git switch -c cmd-compare

# Проверь создание ветки
git branch

# Создай тестовый файл
echo "Test content for switch" > switch-demo.txt
git add switch-demo.txt
git commit -m "Add file for switch demo"

# Вернись на предыдущую ветку (feature/lab2)
git switch -
Switched to branch 'feature/lab2'

# Проверь переключение
git branch
  cmd-compare
  feature/lab1
* feature/lab2
  git-reset-practice
  main
  side-branch
```

##Работа с git checkout
```bash
git checkout -b cmd-compare-2
Switched to a new branch 'cmd-compare-2'
 git branch
  cmd-compare
* cmd-compare-2
  feature/lab1
  feature/lab2
  git-reset-practice
  main
  side-branch
echo "Test content for checkout" > checkout-demo.txt
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git add checkout-demo.txt
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git commit -m "Add file for checkout demo"
[cmd-compare-2 b0a33c2] Add file for checkout demo
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 checkout-demo.txt
 echo "Extra line" >> checkout-demo.txt
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git checkout -- checkout-demo.txt
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> cat checkout-demo.txt
Test content for checkout
```
Работа с git restore
```bash
 git switch feature/lab2
Switched to branch 'feature/lab2'
echo "Initial content" > restore-demo.txt
git add restore-demo.txt
git commit -m "Add file for restore demo"
[feature/lab2 c247506] Add file for restore demo
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 restore-demo.txt

 git status
On branch feature/lab2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   restore-demo.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        et --hard c5e8d1f
        et --soft HEAD~1
        labs/submission2.md
        tatus

no changes added to commit (use "git add" and/or "git commit -a")

git restore restore-demo.txt
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> 
PS C:\Users\aliya\PycharmProjects\DevOps-Intro> git status
On branch feature/lab2
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        et --hard c5e8d1f
        et --soft HEAD~1
        labs/submission2.md
        tatus

nothing added to commit but untracked files present (use "git add" to track)
```

Итог

git switch — используйте для переключения между ветками и создания новых веток. Эта команда специализирована только для работы с ветками, что делает её использование интуитивно понятным и безопасным.

git checkout — устаревшая команда, которую следует избегать, особенно новичкам. Она имеет перегруженную функциональность: переключение веток, создание веток и восстановление файлов, что может привести к путанице и ошибкам.

git restore — используйте для управления состоянием файлов: отмена изменений в рабочей директории, удаление файлов из staged area и восстановление файлов из других коммитов. Эта команда чётко разделяет ответственность и является современной заменой для файловых операций, которые раньше выполнялись через git checkout
# GIT BASIC - PHAN 2

1. [Commit thay doi](#commit-cac-thay-doi)
   - [Commit bo qua staged](#commit-bo-qua-staged)
2. [Removing tep tin](#removing-tep-tin)
3. [Removing cached](#removing-cached)

>

Trong **[ git basic phan 1 ](./git-basic.md)** co de cap de `git dif` de kiem tra thay doi cua mot file da `Staged` va chua `Staged`. Cu the la Demo-100, khi lan dau noi dung cua no duoc Staged va sau do thuc hien chinh sua noi dung nhung khong Stage (Unstaged) va `git diff` thi Git se so sanh noi dung voi noi dung da Staged truoc do cua DEMO-100.

De xem lai nhung thay doi da duoc Staged cho lan `commit` tiep theo so voi lan commit gan nhat truoc do (last commied), ta co the dung git command `git diff --staeged`

```text
$ git diff --staged
diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
+++ b/README
@@ -0,0 +1 @@
+Add content
```

Ket qua cho thay README la mot file moi lan dau duoc them vao Working Tree voi title `new file mode`, sau do da them vao noi dung `Add content` va noi dung thay doi nay da duoc Staged, cuoi cung README chua co lan commit nao voi `/dev/null`.
`git diff --staged` ban than no khong hien thi noi dung thay doi trong lan commit gan nhat (last commited), no chi hien noi dung thay doi da duoc `staged` so voi `last commit`, neu nhu chua co `last commited` nao cho lan thay doi cuoi cung thi no la `/dev/null`.

- ##### Ghi nho:

  - `git diff` chi hien thi ket qua khi thay doi `Unstaged` voi thay doi `Staged` truoc do.
  - `git diff` cung so sanh noi dung `Unstaged` voi `last commited`.
  - `git diff --staged` chi so sanh thay doi da duoc `Staged` so voi `last commited`.

- ##### git diff --cached

  > cach hoat dong cung giong nhu `git diff --staged`, no se thuc hien so so noi dung thay doi `staged` so voi `last commited`

### Commit Cac Thay Doi.

`commit` cac thay doi chi tac dong len nhung thay doi da duoc `staged`, neu nhu co bat ky thay doi nao chua duoc dua vao khu vuc Staging Area (Staged) thi khong duoc commit tiep theo, moi thay doi do chi duoc xem la thay doi tren vung Working Tree - [ 3 trang thai cua git ](./git-three-states.md).

Gia su rang moi thay doi ra duoc Staged va ta thuc hien commit;

> $ git commit

Khi thuc hien `git commit`, Git se hien thi trinh soan thao ma ta da cau hinh trong `git config --global core.editor nano`, trong truong hop nay thi trinh editor `nano` cua he thong se duoc mo dong thoi no se hien thi noi dung output cua `git status` de ta biet duoc noi dung commit se la noi dung gi. Trong trinh soan thao, o tren cung la mot dong trong de nhap `message` cho commit. Noi dung hien thi ben trong Editor se giong nhu the nay:

```text

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Your branch is up-to-date with 'origin/master'.
#
# Changes to be committed:
# new file: README
# modified: DEMO-100
#
~
~
~
".git/COMMIT_EDITMSG" 9L, 283C

```

> Bo het tat ca comments trong Editor va nhap noi dung message de xac nhan commit.

Ngoai ra, de biet chinh xac nhung gi ta se thuc hien commit cho nhung thay doi lan nay, co the them flag `-v`. Flag `-v` se hien thi noi dung cua `git diff --staged` trong trinh soan thao, giup ta biet duoc viec commit se tac dong len nhung thay doi nao.

```text

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
# Changes to be committed:
#       modified:   demo-100
#
# ------------------------ >8 ------------------------
# Do not modify or remove the line above.
# Everything below it will be ignored.
diff --git a/demo-100 b/demo-100
index 1d60b70..02dc432 100644
--- a/demo-100
+++ b/demo-100
@@ -1 +1 @@
-ddd
+eeee
```

Xoa toan bo noi dung trong trinh soan thao, nhap message va xac thuc commit. Thoat ra ngoai bang cach `command + o` de ghi noi dung va `command + x` de thoat, ap dung cho Macbook.

Neu khong muon Git chi dinh Editor de them `message` cho commit, co the them flag `-m` de them `message` ngay tren dong lenh va thuc hien commit

```text
$ git commit -m "first commit"
[master 463dc4f] Story 182: first commit
 2 files changed, 2 insertions(+)
 create mode 100644 README
```

- ##### Commit bo qua Staged

  Nhu da noi, `git commit` chi tac dong len nhung thay doi da duoc Staged. Tuy nhien, doi voi nhung tep file ma Git da `Tracked` thi Git cho phep `commit` truc tiep voi flag `-a` thay vi thuc hien `git add` roi sau do `git commit`. Doi voi nhung file ma Git chua `Tracked` thi phai thuc hien `git add` truoc khi commit.

  Mot dieu luu y, khi cac moi thay doi tren cac file da duoc Git `Tracked`, thi `git commit -a` se commit toan no cac thay doi do. Vay nen can nhac truoc khi su dung, vi mot so thay doi ma ta chua muon thuc hien trong commit hien tai.

  ```text
  # Thuc hien thay doi noi noi dung DEMO-100 va commit
  $ echo "add new content" >> DEMO-100

  # Kiem tra status
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: DEMO-100
  no changes added to commit (use "git add" and/or "git commit -a")

  # commit thay doi
  $ git commit -a -m "commit without staged"
  ```

---

### Removing Tep Tin

Trong ngu canh, kho luu tru dang o trang thai `last commited` chua co bat ky su thay doi nao va toan bo dang duoc Git Tracked. Trong truong hop remove 1 file cu the trong Working Tree, ta co the thuc hien bang cach, mot la lenh Shell va 2 lenh Git. Su khac nhau cua 2 lenh nay la lenh Shell remove dong thoi phai Staged su thay doi, lenh Git remove tu dong Staged su thay doi. Vi du:

```text
$ git-lesson % rm demo3 && git status
On branch main
Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
    deleted:    demo3

no changes added to commit (use "git add" and/or "git commit -a")

$ git-lesson % git rm demo2 && git status
rm 'demo2'
On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
    deleted:    demo2

Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
    deleted:    demo3

```

Trong demo tren thi demo2 va demo3 la 2 file ma Git `Tracked`, khi demo3 xoa bang lenh Shell `rm demo3` nhung chua Staged thay doi. Khi thuc hien remove demo2 bang `git rm` thi Git lam 2 viec `rm demo2` va tu dong `git add demo2`. Ca 2 lenh remove cua Shell va Git chua thuc su lam mat demo3 hay demo 2 hoan toan, vi trong `last commit` gan nhat van con ton tai 2 file nay va co the phuc hoi dua vao du lieu cua `last commit`.

Mot truong hop cu the, khi trong Working Tree hien tai, thuc hien xoa demo3 ra khoi vung lam viec hien tai nhung khong `Staged`. Luc nay demo3 mat tren Working Tree nhung du lieu Git con luu (Dieu kien demo3 nam trong commit gan nhat), ta co the thuc hien khoi phuc demo3 bang cach.

```text
$ rm demo3
$ git status
On branch main
Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git restore <file>..." to discard changes in working directory)
    deleted:    demo3

no changes added to commit (use "git add" and/or "git commit -a")

# Khoi phuc demo3
$ git restore demo3

# List ke tep tin
$ ls -n

```

Cung trong truong hop xoa demo3, nhung truoc khi xoa demo3 ta co thay doi mot so noi dung cho demo3 nhung chua Staged va tiep tuc remove demo3. Khi khoi phuc thi Git se khoi phuc lai demo3 cung voi noi dung goc cua demo3 trong `last commit` cua no. Neu nhu viec thay doi noi dung cho demo3 duoc Staged truoc khi remove thi khi khoi phuc, Git se khoi phuc demo3 cung voi noi dung thay doi da duoc Staged.

```text
$ echo "aaa" >> demo3
$ git add demo3
$ rm demo3

$ git status
On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
    deleted:    demo3

# Khoi phuc demo3
# Dau tien dua demo3 ra khoi vung Staged, du lieu git khoi phuc demo3
# git restore --staged demo3

# Khoi phuc demo3 cho Working Tree
$ git restore demo3

# List item kiem tra demo3 restored chua
# ls -n

# Test noi dung demo3
# cat demo3
```

Neu nhu mot file moi duoc them vao Working Tree va chua duoc Git Tracked, thi khi khong the thuc hien remove bang lenh Git, dieu nay cung dong nghia khi thuc hien remove bang lenh Shell thi file do se bien mat trong Wroking Tree va Git cung khong the phuc hoi duoc file do. Neu nhu file duoc them vao va Staged thi khi remove bang Shell thi Git se phuc hoi file do tu khu vuc Staged.

> Them file demo4 nhung Untracked

```text
$ touch demo4
$ git status
$ rm demo4
$ git restore demo4
error: pathspec 'demo4' did not match any file(s) known to git
```

> Them file demo4 nhung Tracked

```text
$ touch demo4
$ git add demo4
$ git status

# Xoa bang lenh Shell
$ rm demo4

$ ls | grep demo4

$ git restore demo4
$ ls -n | grep demo4
```

Gia su rang, demo4 sau khi duoc Git phuc hoi tu vung Staging, tiep tuc thuc hien `rm demo4` va `git add demo4` va `git status`, ket qua la Working Tree ve lai trang thai cua `last commit` chua co demo4.

Cung trong truong hop demo4 sau khi khoi phuc tu vung Staging, thuc hien `git rm` va `git status`, ta co ket qua:

```text
$ git-lesson % git rm demo4
error: the following file has changes staged in the index:
    demo4
(use --cached to keep the file, or -f to force removal)
```

Output la 1 thong bao loi va mot loi nhac. Theo dung logic thi Working Tree se tra ve trang thai `last commit` vi lenh `git rm` no lam 2 viec la `rm demo4` va `git add demo4` nhung lai la mot thong bao loi. Van de nay nam o cho, khi `git rm` thi Git kiem tra trong `last commit` co ton tai demo4 chua, neu demo4 da ton tai thi no se remove demo4 va khong thong bao loi vi sau khi remove Git co the phuc hoi dua vao du lieu `last commited`, va neu demo4 chua co trong `last commited` thi Git thong bao loi, dieu nay dam bao cho tinh an toan du lieu khong bi xoa nham vi nhieu khi demo4 co du lieu quan trong chua duoc commit nhung lo remove mac du da Staged thi thong bao loi la cach de giu an toan cho du lieu trong demo4.

Nhu vay, trong moi truong hop doi khi `remove` mot file nao do, can can nhac dung lenh Shell hay lenh Git de dam bao an toan cho du lieu.

`git rm` co the cho phep truyn vao pattern de remove moi thu, nhung can than.

```bash
# Xoa tat ca file/subdir trong thu muc temp tai current directory
$ git rm ./temp/**

# Xoa tat ca file .log nam trong thu muc log, nhung khong duoc xoa .log nam trong subdir cua log.
$ git rm log/\*.log
```

Dau `\` truoc `*` co nghia la ngan khong cho Shell mo rong `*`, vi `git mr` no thuc hien `rm file-name` va `git add`, cho nen dau `\` truoc ky tu `*` se ngan hanh vi mo rong cua Shell.

---

### Removing Cached

`Removing cache` la tinh nang giup cho viec huy theo doi cua Git doi voi mot file cu the. Trong truong hop cu the, khi vo tinh dua mot file chua thong tin nhay cam vao vung Staging (Staged) cho commit sap toi, viec huy bo no la dieu can thiet de tranh commit thong tin cua file khong mong muon. Git cho phep huuy theo theo tep do bang command `git rm --cached file`.

Neu nhu file do chi moi duoc dua vao vung Staging (Staged) nhung chua commit, thi `git resstore --staged` se dua file do ra khoi vung Staging va bo theo doi. Neu file do da nam trong mot commit cu the thi `git rm --cached` se giai quyet van de huy Trackied. Vi du:

> file .env chua commit

```bash
# Staged toan bbo thay doi
$ git add .

# Remove .env ra khoi vung Staged
$ git restore --staged .env

$ git status
```

> file .env vo tinh nam trong mot commit truoc do hoac lo commited cho thay doi hien tai

```bash
# Remove .env ra khoi index du lieu Git
$ git rm --cached .env

# Kiem tra lai trang thai .env
$ git status
```

### Moving File

Moving file la lenh di chuyen file tu thu muc nay sang thu muc khac, tuy nhien `moving` cung duoc dung de thay doi ten cua mot file. Moving trong Git cung giong lenh `move` trong Shell.

Trong Git, khi thay doi ten cua mot File, ta co the su dung `git mv` de thuc hien do

```text
$ git mv README.md README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
  renamed: README.md -> README
```

Khi thuc hien doi ten file bang `git mv`, Git tu dong Staged thay doi do. Neu dung shell de thay doi ten file thi ta can phai thuc hien 3 buoc

```text
# Doi ten file
$ mv README.md README

# Remove file README.md ma git Tracked
$ git rm README.md

# Add file moi moi doi ten README va Staged
$ git add README
```

Viec doi ten file trong Git co the duoc thuc hien theo nhieu cong cu khac nhau, nhung neu thuc hien bang lenh cua Git thi ta chi can thuc hien 1 buoc thay vi 3 buoc truoc khi commit.

- **[ Git basic phan 3 ](./git-basic-3.md) - [ Ve dau trang ](#git-basic---phan-2)**

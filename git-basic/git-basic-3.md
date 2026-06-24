# GIT BASIC - PHAN 3

1. [Git log - Xem lich su committed](#viewing-git-log---xem-lich-su-commit)
   - [Mau pattern format](#bang-ky-hieu-pattern-cho---prettyformat)
   - [Mau Optional](#bang-optiional-cho-git-log)
2. [Undoing Things - Hoan Tac](#undoing---hoan-tac)
3. [Unstaged tep tin](#unstage-a-staged-file---hoan-tac-mot-file-staged)

>

### Viewing Git Log - Xem Lich Su Commit

Sau khi thuc hien mot so commit hoac khi clone kho luu tru co san, Git cho phep xem lai toan bo lich su commit cua kho luu tru do. su dung `git log` de lam dieu do. Mac dinh, `git log` chi hien thi noi dung cua cua commit, vi du:

```text
$ git log
commit d09672744cd826bde08a04b8b6c9a515c10b9439 (HEAD -> main)
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:39:21 2026 +0700

    fourth committed

commit 5a242f560b433e344895245d18eb0f955aff46f8
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:20:59 2026 +0700

    third committed
...
```

Co the them tuy chon `-p` (--patch) de xem noi dung thay doi cua tung commit va gioi han so luong log bang tham so [-number] neu khong muon xem toan bo lich su commit, vi du:

```text
$ git log -p -2
commit d09672744cd826bde08a04b8b6c9a515c10b9439 (HEAD -> main)
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:39:21 2026 +0700

    fourth committed

diff --git a/demo-100 b/demo-100
index 1d60b70..02dc432 100644
--- a/demo-100
+++ b/demo-100
@@ -1 +1 @@
-ddd
+eeee

commit 5a242f560b433e344895245d18eb0f955aff46f8
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:20:59 2026 +0700

    third committed

diff --git a/demo-100 b/demo-100
index aa921fd..1d60b70 100644
--- a/demo-100
+++ b/demo-100
@@ -1,3 +1 @@
-aaa
-bbbb
-ccc
+ddd
```

Tuy chon `-p` hien thi toan bo ket qua, nhung gia da dien ra cua mot commit, co the xem cac thay doi truc ngay trong nhat ky. Dieu nay can thiet khi muon xem nhung gi da xay ra trong mot commit cu the.
Neu nhu muon xem mot so thong ke duoc rut gon cho moi commit thi co the dung tham so tuy chon `--stat` va `-number` de gioi han so luong log.

```text
$ git log --stat -2
commit d09672744cd826bde08a04b8b6c9a515c10b9439 (HEAD -> main)
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:39:21 2026 +0700

    fourth committed

 demo-100 | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

commit 5a242f560b433e344895245d18eb0f955aff46f8
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Sun Jun 21 08:20:59 2026 +0700

    third committed

 demo-100 | 4 +---
 1 file changed, 1 insertion(+), 3 deletions(-)
```

Output cua `--stat` cho ta biet duoc cac thong tin noi dung cua mot commit, dong thoi cho ta biet co bao nhieu file da thay doi, va tong so dong thay doi la bao nhieu. Trong vi du nay, o commit "third committed" cho ta biet file demo-100 co tong so dong thay doi la 4, trong do 1 them moi va 3 da bi xoa, tong so file bi thay doi trong commit nay la 1 [demo-100].

`--pretty`, tuy chon nay co the thay doi format ouput mac dinh cua Git, `oneline` la gia tri cho tuy chon `--pretty` duoc tao san boi Git, no cho phep ket qua hien thi tren 1 dong cua moi commit. Ngoai ra, cac gia tri short, full va fuller hien thi format output gan giong nhau nhung voi it hoac nhieu thong hon. Vi du:

```text
$ git log --pretty=oneline
d09672744cd826bde08a04b8b6c9a515c10b9439 (HEAD -> main) fourth committed
5a242f560b433e344895245d18eb0f955aff46f8 third committed
54215e02abf45bebe24d85a00ddb47bcc9bc4923 add ccc
952aa44bdd99488ea7e698ed864b73103076908c add bbb for demo-100
48b4ca9aa636e0cc165e8319900d5e821c82f4bb add demo-100
955a9723bf79cd5da71e84f7ce86530cd847b117 ok
c9c85eac7a03b8079384f0847b2eaa0ab7a8d7fe Merge branch 'daitran'
bc344483d0a344b367e197451ca8c0383f04b984 (tag: v1.1, daitran) them noi dung
51ff886c19ab9909da28419bcd3e39ee04b2ce91 (tag: v3.0) third commit
69d0c7efeab5c4765899ea2fb65bc74860e698a9 (tag: v2.0) second commit
feb34f3d65cc0178ef360b531d43030282a10509 (tag: v1.0) first commit
```

Hoac cung co the su dung gia tri `format` cho tuy chon `--pretty` de format lai thong tin commit

```text
$ git log --pretty=format:"%h - %an, %ar : %s"
d096727 - Quangdai2207, 21 hours ago : fourth commitrd
5a242f5 - Quangdai2207, 21 hours ago : third committed
54215e0 - Quangdai2207, 22 hours ago : add ccc
952aa44 - Quangdai2207, 22 hours ago : add bbb for demo-100
48b4ca9 - Quangdai2207, 22 hours ago : add demo-100
955a972 - Quangdai2207, 2 days ago : ok
c9c85ea - Quangdai2207, 10 days ago : Merge branch 'daitran'
bc34448 - Quangdai2207, 10 days ago : them noi dung
51ff886 - Quangdai2207, 10 days ago : third commit
69d0c7e - Quangdai2207, 10 days ago : second commit
feb34f3 - Quangdai2207, 10 days ago : first commit
```

- #### Bang ky hieu Pattern cho --pretty=format

  <table border=2>
        <thead style="font-weight:bold; font-size:16px">
            <th align="left">Pattern</th>
            <th align="left">Y nghia</th>
        </thead>
        <tbody style="font-weight:bold; font-size:16px">
            <tr>
                <td>%H</td>
                <td>Commit hash</td>
            </tr>
            <tr>
                <td>%h</td>
                <td>Ma hash rut gon cua commit</td>
            </tr>
            <tr>
                <td>%T</td>
                <td>Ma hash cua tree</td>
            </tr>
            <tr>
                <td>%t</td>
                <td>Ma hash rut gon cua Tree</td>
            </tr>
            <tr>
                <td>%P</td>
                <td>Ma hash cua commit cha</td>
            </tr>
            <tr>
                <td>%p</td>
                <td>Ma hash rut gon cua commit cha</td>
            </tr>
            <tr>
                <td>%an</td>
                <td>Ten cua tac gia commit</td>
            </tr>
            <tr>
                <td>%ae</td>
                <td>Email cua tac gia commit</td>
            </tr>
            <tr>
                <td>%ad</td>
                <td>Ngay xuat ban, (dinh dang theo tuy chon --date=option)</td>
            </tr>
            <tr>
                <td>%ar</td>
                <td>Tac gia, ngay, tuong doi</td>
            </tr>
            <tr>
                <td>%cn</td>
                <td>Ten nguoi commit</td>
            </tr>
            <tr>
                <td>%ce</td>
                <td>Email nguoi Commit</td>
            </tr>
            <tr>
                <td>%cd</td>
                <td>Ngay commit</td>
            </tr>
            <tr>
                <td>%cr</td>
                <td>Ngay commit, tuong doi</td>
            </tr>
            <tr>
                <td>%s</td>
                <td>Chu de</td>
            </tr>
        </tbody>
    </table>

Co the ket hop `--pretty=format` va `--oneline` voi tuy chon `--graph` de xem lich su commit dang Tree

```text
* d096727 (HEAD -> main) fourth committed
* 5a242f5 third committed
* 54215e0 add ccc
* 952aa44 add bbb for demo-100
* 48b4ca9 add demo-100
* 955a972 ok
*   c9c85ea Merge branch 'daitran'
|\
| * bc34448 (tag: v1.1, daitran) them noi dung
* | 51ff886 (tag: v3.0) third commit
* | 69d0c7e (tag: v2.0) second commit
|/
* feb34f3 (tag: v1.0) first commit
```

Ket qua dau ra cho biet lich su cua qua trinh tach nhanh va `merge commit` duoc dien ra nhu the nao. Trong truong hop nay. tai commit goc dau tien "first commit" tiep dien len commit `51ff886 - thrid commit`, ngay tai `first commit - feb34f3` co mot nhanh `daitran - bc34448`, cuoi cung la merge commit tai `c9c85ea` va tiep tuc cac commit con lai phat trien tren nhanh `main`. HEAD la con tro cho ta biet no dang dung `last committed` va tren nhanh `main`.

- #### Bang optiional cho `git log`

  | Optional        | Y nghia                                                                                              |
  | --------------- | ---------------------------------------------------------------------------------------------------- |
  | -p              | Hien thi ban va cho moi commit                                                                       |
  | --stat          | Hien thi so lieu thong ke cho moi commit                                                             |
  | --shortstat     | Hien thi so dong da thay doi/chen/xoa tu lenh --stat                                                 |
  | --name-only     | Hien thi danh sach cac tep tin duoc sua doi sau thong tin commit                                     |
  | --name-status   | Hien thi danh sach tep bi anh huongvoi thong tin duoc them/sua/xoa                                   |
  | --abbrev-commit | Chi hien thi mot vai ky tu dau tien cua tong kiem tra SHA-1 thay vi 40 ky tu                         |
  | --relative-date | Hien thi ngay co format tuong doi (VD: "2 tuan truoc") thay vi hien thi ngay day du                  |
  | --graph         | Hien thi graph dang ASCII cua nhanh va lich su merge commit kem voi noi dung log                     |
  | --pretty        | Hien thi commit o dinh dang custom. Cac gia tri tuy chon format bao gom oneline, short, full, fuller |
  | --oneline       | Viet tat cua --pretty=oneline --abbrev-commit su dung ket hop                                        |

  Mot so cac tuy chon ve gioi han thoi gian `time-limiting` cung co them mot so thong tin huu ich khi muon xem nhat ky commit

  ```text
  $ git log --since=1.week --oneline
  d096727 (HEAD -> main) fourth committed
  5a242f5 third committed
  54215e0 add ccc
  952aa44 add bbb for demo-100
  48b4ca9 add demo-100
  955a972 ok

  # Hoac dung format --since="[<yy-mm-dd> | <time ago> | <2 year 3 days 10 minutes>]"
  $ git log --since="24 hours ago"
  d096727 (HEAD -> main) fourth committed
  5a242f5 third committed

  # Hoac ket hop voi lenh Shell bash
  $ git log --pretty=format:"%h - %ae" -2 | grep -e "ai"
  d096727 - daitran.inbox@gmail.com
  5a242f5 - daitran.inbox@gmail.com
  ```

  ```bash
  # Chi muon xem cac commit cu the cua mot file/folder, dung (-- de thuc hien
  $ git log -- git-deeper/demo-100

  # Chi muon xem commit cua mot noi dung (function, chuoii), neu biet cu the chuoi hoac ham chuc nang do, dung -S thuc hien
  $ git log -S userService
  ```

  | Optional          | Y nghia                                                                    |
  | ----------------- | -------------------------------------------------------------------------- |
  | -<n>              | Hien thi n commit, tinh tu last commit tro ve truoc                        |
  | --since, --after  | gioi han commit da tao sau ngay dinh dinh (Ke tu ngay.....den sau ngay)    |
  | --until, --before | Gioi han commit da tao truoc ngay chi dinh (Ke tu ngay.... den truoc ngay) |
  | --author          | Hien thi commit khoi voi ten cua tac gia                                   |
  | --committer       | Chi hien thi commit khoi voi ten nguoi commit                              |
  | --grep            | Chi hien thi commit khop voi chuoi message                                 |
  | -S                | Hien thi commits khop voi chuoi chi dinh                                   |

  ```bash
  # lay 5 commit chua merge tai thu muc src/ ke tu 01-05-2026 den truoc 01-06-2026 voi format [hash - author - date]
  $ git log --pretty=format:"%h - %ad" --oneline -- since="2026-05-01" --before="2026-06-01" --no-merges -- src/ -5
  ```

### Undoing - Hoan tac

Tai moi giai doan, doi luc thuc hien sai commit hoac commit sot noi dung trong qua trinh lam ta cung deu can thuc hien hoan tac mot so thuc de thuc hien lai commit. `--amend` se thuc hien dieu do neu nhu mot commit khong dung nhu mong muon.

```bash
# them noi dung cho demo3
$ echo "them noi dung" > demmo3

# commit sai thong diep
$ git commit -am "themm noi dung demo2"

# Log nhat ky
$ git log -3

# Undo commit loi demo3 thay vi demo2 va loi typo "themm"
$ git commit --amend -m "them noi dung demo3"
```

`commit --amend` no chi thuc thi cho `last commit`, nhu trong vi du, commit sau thong diep la `last commit` tai thoi diem do va `--amend` chi thuc thi tren commit loi do. Die quan trong la khi `--amend` sua loi cho `last commit` khong mong muon thi `last commit` no khong bien mat vi commit duoc tao la bat bien, khong the thay doi - [ xem lai git basic ](./Understanding-git.md), chi la con tro HEAD dich chuyen qua commit `--amend`. Su dung `git reflog` de kiem tra:

```text
$ git reflog -5
a406d8c (HEAD -> main) HEAD@{0}: commit (amend): Them noi dung cho demo3
1b0563c HEAD@{1}: commit (amend): them noi dung cho demo3
80bafeb HEAD@{2}: commit: themm noi dung demo2
d096727 HEAD@{3}: commit: fourth committed
5a242f5 HEAD@{4}: commit: third committed
```

> --amend la cach thay the commit cu ra khoi lich su commit cua kho luu tru thong thuong

### Unstage A Staged File - Hoan Tac Mot File Staged

Unsstaging la viec dua mot file ra khoi khu vuc Staging- [ 3 trang thai cua Git ](./git-three-states.md). Viec dua mot file ra khoi khu vuc Staging (Unstaged) khong co nghia la file do khong con su theo doi (Untracked) cua Git tru khi file do chua co trong `last committed`. Trong qua trinh lam viec, doi khi bi nham lan khi dua mot file khong mong muon vao khu vuc Staging, ta co the phuc hoi bang cach `git restore` hoac `git reset` de thuc hien

```text
$ echo "noi dung moi demo3" >> demo3
$ echo "noi dung moi demo2" >> demo2

# Staged thay doi
$ git add .

# Kiem tra
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   demo2
	modified:   demo3


# Unstaged demo2
$ git restore --staged demo2

# Kiem tra
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   demo3

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   demo2
```

khi thuc hien `git status`, trong output Git co goi y viec su dung `(use "git restore --staged <file>..." to unstage)` cho demo3 ra khoi khu vuc Staging va `(use "git restore <file>..." to discard changes in working directory)` khoi phuc lai noi dung demo2.

```text
$ cat demo2
noi dung moi demo2

# khoi phuc lai noi dung truoc khi them "noi dung moi demo2"
$ git restore demo2

$ cat demo2

```

> **Luu y:** Neu mot file da chinh sua nhung chua Staged, khi "git restore" toan bo noi dung chinh sua se bien mat va noi dung file se quay ve noi dung cua "last commit".

Gia su, noi dung moi cua demo3 da duoc committed nhung vi li do nao do ta muon huy bo commit do, thi ta co the thuc hien

```text
$ git reset --hard HEAD^
HEAD is now at 0dc914e add content demo3

$ git status
commit 0dc914e228ec0c4528bbb9cfa1ea26533b98aa1c (HEAD -> main)
Author: Quangdai2207 <daitran.inbox@gmail.com>
Date:   Mon Jun 22 10:10:30 2026 +0700

    add content demo3

diff --git a/demo3 b/demo3
index 63aefe1..2e56c50 100644
--- a/demo3
+++ b/demo3
@@ -1 +1,2 @@
 kkk
+aabb
```

Lenh `git reset --hard HEAD^` chi tac dong len `last committed` vi con tro `HEAD^` bieu thi cho `last committed` ma HEAD dang dung. Khi lenh nay duoc thuc thi thi Git lam 3 viec:

> 1. Git reset lai index va Workiing trong du lieu cua Git
> 2. Git di chuyen con tro HEAD xuong commit gan nhat, (0dc914e228ec0c4528bbb9cfa1ea26533b98aa1c)
> 3. Toan bo noi dung thay doi trong demo3 duoc restore ve commit gan nhat (0dc914e228ec0c4528bbb9cfa1ea26533b98aa1c)

Khi su dung lenh nay tuyet doi can than, chi su dung trong truong hop thuc su can thiet. Mot cach an toan co the khac phuc su co khong mong muon la backup toan bo noi dung ra mot file rieng khong bi Git Tracked hoac nam trong mot Folder doc lap khac. Sau khi backup an toan thi thuc hien lenh `git reset`.

- ###### [Ve dau trang](#git-basic---phan-3) - [ Git basic phan 4 ](./git-basic-4.md)

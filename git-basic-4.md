# GIT BASIC - PHAN 4

### Woking Tree Remote - Vung lam viec Remote

Remote la mot kho luu tru tu xa, noi quan ly toan bo ma nguon cua mot du an hoac don gian chi la kho tai lieu ma ta muon luu tru. Kho luu truc remote co the chi co mot hoac nhieu thanh vien cung truy cap vao no va thuc hien doc/ghi. Nhung nguoi tham gia co the pull/push/clone khi can chia se cong viec chung. Khi lam viec voi kho luu tru tu xa can phai biet cach quan ly no, biet cach them remote, quan ly cac nhanh lam viec son song va trang thai cua remote...vv.

Tren thuc te, khi Remote cung co the nam ngay tren thiet bi cua chung ta chu khong nhat thiet nam dau do tren Internet. De giai thich cho viec nay, gia su trong cung mot mang Lan, mot nhom co 5 nguoi cung lam viec tren mot ma nguon. Trong do, mot nguoi tinh nguyen dong vai tro la kho luu tru Remote cho 4 thanh vien khac co the truy cap thong qua giao thuc SSH hoac HTTP. Nhu vay, thiet bi nguoi dong vai tro la remote ho co the tuong tac voi remote truc tiep ngay tren thiet bi cua ho hoac ung dung `gogs` cung la mot trong nhung remote local ngay tren thiet bi.

### Showing Remotes - Hien Thi Cac Remotes

De biet duoc ta dang tuong tac voi remote nao, su dung `git remote` de kiem tra;

```text
$ git remote
$ myLab % git remote
origin

$ myLab % git remote -v
origin	git@github.com:Quangdai2207/GIT_LESSON.git (fetch)
origin	git@github.com:Quangdai2207/GIT_LESSON.git (push)
```

Output cho ta biet duoc ta dang `origin` la kho remote ma ta tuong tac, `-v` cho ta biet chi tiet `URL` cua Remote `origin`.

Mot tai nguyen/ du an co the co nhieu kho luu tru khac nhau cho muc dich backup hoac tinh chat quan trong. Mot local cung co the co nhieu Remote de lam viec.

```text
$ cd myLab
$ git remote -v
local http://localhost:3000/account/GIT_LESSON (fetch)
local http://localhost:3000/account/GIT_LESSON (push)
corigin	https://github.com/Quangdai2207/GIT_LESSON.git (fetch)
origin	https://github.com/Quangdai2207/GIT_LESSON.git (push)
teamwork https://github.com/Quangdai2207/git-handbook.git (fetch)
teamwork https://github.com/Quangdai2207/git-handbook.git (push)
```

Output cho ta biet hien tai dang tuong tac voi 3 remote `origin`, `local`, `teamwork`, ung voi moi Remote la URL tuong ung cua Remote ma ta dang lam viec.

### Adding Remote Repositories - Them Remote Cho Repositores

Co the them nhieu Remote cho 1 repository hoac cung co the them Remote cho mot Repository hua duoc Remote

```text
# Them Remote cho mot Repository da Remoted
$ git remote add origin git@github.com:Quangdai2207/GIT_LESSON.git

$ git remote -v
git-lesson	https://github.com/Quangdai2207/GIT_LESSON.git (fetch)
git-lesson	https://github.com/Quangdai2207/GIT_LESSON.git (push)
origin	https://github.com/Quangdai2207/GIT_LESSON.git (fetch)
origin	https://github.com/Quangdai2207/GIT_LESSON.git (push)

# Them Remote cho mot Repository chua remoted
$ git remote add local5000 http://localhost:5000/account/document

$ git remote -v
git-lesson	https://github.com/Quangdai2207/GIT_LESSON.git (fetch)
git-lesson	https://github.com/Quangdai2207/GIT_LESSON.git (push)
origin	https://github.com/Quangdai2207/GIT_LESSON.git (fetch)
origin	https://github.com/Quangdai2207/GIT_LESSON.git (push)
local5000	https://localhost:5000/account/document (fetch)
local5000	https://localhost:5000/account/document (push)
```

Thuc hien nap du lieu cap nhat trang thai kho du lieu tu Remote cho local, su dung ten remote de thuc Fetch du lieu

```text
$ git fetch git-lesson
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.72 KiB | 440.00 KiB/s, done.
From github.com:Quangdai2207/GIT_LESSON
   a1702fd..7572c39  main       -> git-lesson/main
```

Ket qua output cho ta biet toan bo du lieu tren nhanh `main` cua Remote Repo da duoc nap cho kho luu tru local. Sau khi Fetch du lieu thanh cong, du lieu chi cap nhat kho luu tru cuc bo ma thoi, cu the la `.git` cua ban co du lieu, nhung Working Directory van hoan toan chua co du lieu. De du lieu hien thi tren Working Directory ta can thuc hien them mot buoc la `merge`, va ta se `merge` bang `Remote tracking - git-lesson/main`. **Remote tracking** se duoc giai thich sau.

```text
$ git merge git-lesson/main
Updating a1702fd..7572c39
Fast-forward
 git-lesson.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 git-lesson.md

$ git status
 On branch main
 nothing to commit, working tree clean
```

### Fetching And Pulling Remote - Nap va Keo Du Lieu Tu Remote

> $ git fetch <remote>

Khi su dung cau lenh nay, thi no se thuc hien viec tai toan bo du lieu tu kho luu tru Remote, bat ky du lieu nao duoc pushed len kho Remote cung duoc tai ve trong kho luu tru cuc bo cua ban (.git). Sau khi thuc hien xong, kho luu tru cuc bo se co toan bo lich su commit va cac nhanh hien co cua kho luu tru Remote va co the merge thu cong bat cu khi nao ban muon.

Mac dinh, khi lan dau `clone` mot kho luu tru co san, Git se tu dong them Remote vao cho kho luu tru do co ten la `origin`. Do do, `git feftch origin` no se nap bat ky du lieu nao duoc Pushed ke tu luc ban `cloned` hoac Fetched lan moi nhat. Nhung quan trong rang, Fetch no chi nap du lieu tu kho remote vao trong kho du lieu local (.git) chu khong tu dong `merge` vao vung lam viec hien tai cua ban, tinh huong nay can phai `merge` thu cong va co the merge vao bat ky thoi diem nao ban ban cam thay san sang lam viec voi no.

Mot dieu nua, khi lan dau `clone` kho luu tru tu xa ve tren may, Git se tu dong tao mot nhanh `main` cho kho luu tru local, dong thoi nhanh `main` nay cung duoc thiet lap the Tracking nhanh `main` cua kho luu tru Remote thong qua Branch Tracking, dong thoi kho luu tru cuc bo tu dong duoc Git thiet lap theo doi trang thai cua kho luu tru Remote thong qua Remote Tracking. Ca 2 doi tuong `Branch Tracking va Remote Tracking` deu co dang `<Remote>/<Branch> - git-lesson/main`. Diem giong va khac se duoc giai thich sau.

Sau khi nhanh `main` cua kho luu tru local duoc Git thiet lap 2 doi tuong Tracking, co the su dung cau lenh `git pull` de thuc hien `fetch` va `merge` du lieu vao local cho ban.

Ke tu phien ban `Git 2.27` tro ve sau, Git se canh bao ve viec `pull` du lieu tu Remote. Neu ban chi muon merge theo cach thong thuong thi co the dung `git pull`, con neu muon rebase thi co the dung `git pull --rebase`.

```bash
# Cau hinh git pull mac dinh
$ git config --global pull.rebase "false"

# Cau hinh pull --rebase
$ git config --global pull.rebase "true"
```

> Luu y: Khi thuc hien cau hinh mac dinh pull.rebase "true" thi nen can than voi lenh 'git pull', vi 'git pull' luc nay se la 'git pull --rebase'

```text
# pull la true
$ git pull git-lessoon/main  <=> git pull --rebase <remote>/<branch>
```

Khi thuc hien `git pull <remote>` hoac `git pull --rebase <remote>`, Git se thuc hien 2 dieu:

> ##### git pull origin
>
> 1. git fetch origin
> 2. git merge origin/main

> ##### git pull --rebase origin
>
> 1. git fetch origin
> 2. git rebase origin/main

Neu trong qua trinh lam viec, flow dang la `git pull` go nham lenh `git pull --rebase` hoac nguoc lai, thi `git reset` se phuc hoi lai kho luu tru cuc bo ve lai trang thai truoc khi Fetch du lieu;

```bash
# Phuc hoi trang thai kho luu truc cuc bo ve trang thai truoc khi fetch
$ git reset --hard HEAD~1

# Thuc hien lai git pull dung flow khong rebase
$ git pull origin
```

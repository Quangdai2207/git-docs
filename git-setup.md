# CAU HINH GIT

Sau khi cai dat Git tren he thong, ta can thuc hien mot so thiet lap de tuy chinh moi truong cho Git tren he thong. Cac thiet lap nay chi can khia bao mot lan tren bat ky may tinh nao ca chung duoc giu nguyen giua cac lan nang cap version cua Git. Cac thiet lap nay co the thay doi bat ky luc nao bang cach chay lai cac lenh.

1. [Cac cap do cau hinh GIT](#cac-cap-do-cau-hinh-git)
2. [Kiem tra thong tin cau hinh](#kiem-tra-thong-tin-cau-hinh)
3. [Thiet lap cau hinh](#thiet-lap-thong-tin-cau-hinh)
4. [GIT help](#git-help)

---

## Cac cap do Cau hinh Git

Mot cong cu cho phep thuc hien cac thiet lap Git la `git config`, lenh nay cho phep lay va theit lap cac bien cau hinh kiem soat tat ca cac khia canh ve giao dien va hoat dong cua Git. Cac bien co the duoc luu o 3 vi tri khac nhau:

- 1. `/etc/gitconfig` file:
     file chua cac gia tri duoc ap dung cho moi nguoi dung tren he thong va tat ca cac kho chua cua nguoi dung. Neu truyen vao them tuy chon `--system` cho `git config`, no se doc va ghi tu file nay. Boi vi, file nay la file cau hinh he thong, ta se can phai quan tri hoac quyen cua **superuser** de co the thay doi duoc cac gia tri cua chung. Day la file cau hinh o cap do he thong.

- 2. `~/.gitconfig` or `~/.config/git/config` file:
     Cac gia tri danh rieng cho ban, nguoi dung. Ban o the cho phep Git doc va ghi vao trong file nay bang cach truyen vao tuy chon `--global`, va dieu nay no se nah huong den tat ca cac kho luu tru ma ban dang lam viec tren he thong. Day la file cau hinh cap do danh nguoi dung hien tai.

- 3. `config` file trong Git directory (tuc la `.git/conig`) cua bat ky kho chua nao ma ban dang dung hien tai va tep nay chi danh rieng cho kho luu tru do. Ta co the buoc Git phai doc va ghi file nay bang cach them vao tuy chon `--local` nhung thuc chat day la tuy chon mac dinh. De no co the hoat dong dung cach thi ta can phai trong mot kho luu tru nao do cu the. Day la file cau hinh cap do local tren mot `.git` repository cu the

Trong tung ngu canh cu the, Git se ghi de gia tri cau hinh len gia tri cua cap do tren no. Vi du,

- System - `/etc/gitconfig` tai **root**
- User - `~/.gitconfig` hoac `~/.config/git/config` tai **$HOME** nguoi dung
- Local - `.git/config` trong mot **project** cu the

## Kiem Tra Thong Tin Cau Hinh

Mac dinh, khi trong moi truong Git dang hoat dong neu khong co bat ky gia tri cau hinh nao duoc thiet lap thi Git se lay gia tri cua cap do tren no de ap dung (ap do cao gan moi truong Git dang hoat dong nhat). Neu moi truong hien tai cua Git duoc thiet lap cau hinh thi cac gia tri nay se ghi de len gia tri cua cap tren no.

`cd` ve root `/` hoac `$HOME` hoac `my-project`, ung voi mot Working Directory cu the, su dung lenh git config de kiem tra Git dang lay gia tri cua file cau hinh nao

```bash
# Gia du dang dung tai $HOME cua nguoi dung tren may Mac
# Kiem tra user.name lay tu file cau hinh nao
$ git config --show-origin user.name
```

**Output:**

> file:/Users/admin/.gitconfig username

Output la file cau hinh `/Users/admin/.gitconfig` tai $HOME cua nguoi dung, day la cap do cau hinh Global, Moi cau hinh tai Global se anh huong den qua trinh hoat dong cua Git.

Liet ke toan bo thong tin cau hinh cua cac cap do trong moi truong hien tai, su dung `git config`:

```bash
# Liet ke toan bo thong tin cau hinh (Ca 3 cap do)
$ git config --list --show-origin
```

## Thiet Lap Thong Tin Cau Hinh

Ban dau, muon khai bao cau hinh Git cho he thong 1 lan duy nhat ta co the su dung flag `--global` cho tep cau hinh chung tai khu vuc `$HOME` Working Directory cua nguoi dung

```bash
# Thiet lap ten nguoi dung cho Git
$ git config --global user.name "username"

# Thiet lap email nguoi dung cho Git
$ git config --global user.email "example@gmail.com"
```

Tren thuc the tuy tung truong hop ma thiet lap cau hinh Git phu hop cho tung ngu canh. Vi du, mot to chuc doanh nghiep co nhieu ung dung va kho luu tru cua ung dung do, ung voi moi kho luu tru yeu cau cau hinh khac nhau de su dung cho kho luu tru do, nen viec cau hinh `local` cu the cho tung kho luu tru la dieu can thiet vi muc dich cu the kho luu tru do.

Gia su khi clone project tu cong ty, cong ty yeu cau `account` noi bo de push/pull code, ta co the thuc hien:

```bash
# cd vao du an cong ty
$ cd project-company

# Thiet lap cau hinh noi bo cho du an
$ git config --local user.name "Adam-Nguyen"
$ git config --local user.email "adamnguyen@company.com"
```

Ngoai ra, con co the cau hinh chi dinh trinh soan thao Editor khi Git can su dung de soan thao message. Neu khong co thong tin cau hinh Editor, Git se dung chuong trinh mac dinh cua he thong. Su dung thuoc tinh `core.editor` cho cau hinh Editor:

```bash
# Co the thay Editor khac cho Git su dung
$ git config --glocal core.editor emacs
```

Khi khoi tao repository cuc bo bang `git init`, mac dinh Git se tao mot ten nhanh co ten `master`. Tu phien ban `version 2.28` Git cho phep doi ten nhanh mac dinh tuy y thay vi mac dinh la `master`

```bash
# Thay doi ten nhanh chinh la "main" thay vi "master"
$ git config --glocal init.defaultBranch main
```

Sau khi cau hinh xong, co the xem lai thong tin cac cau hinh vua moi thiet lap bang lenh `git config --list`

```bash
$ git config --list
```

Khong nhu cau lenh co flag `--show-origin`, `--list` chi liet ke thong tin cau hinh la cac `KEY=VALUE` khong bao gom cac `path` cu the cua tung `KEY = VALUE`, nhung ta can ngam hieu rang GIT se tu ap dung cau hinh trong ngu canh moi truong hien tai cua no duoc thiet lap. Git cung cho phep doc cau hinh cu the cua mot thuoc tinh

```bash
# Doc username tu thuoc tinh user.name
$ git config user.name

# Doc email tu thuoc tinh user.email
$ git config user.email
```

**Output:**

> username

> example@gmail.com

## GIT Help

Co 4 cu phap chinh de xem huong dan GIT trong qua trinh su dung

```text
git help <verb>
git <verb> --help
git <verb> -h
man git
```

Vi du:

```bash
# Huong dan chung ve GIT bang help
$ git help

# Huong dan du dung Git bang chuong trinh "man"
$ man git

# Huong dan mot command cu the cua GIT
$ git config --help
$ git config -h
$ git help config
```

Thong tin huong dan GIT co dang nhu sau:

```text
$ git add -h
usage: git add [<options>] [--] <pathspec>...
      -n, --dry-run dry run
      -v, --verbose be verbose
      -i, --interactive interactive picking
      -p, --patch select hunks interactively
      -e, --edit edit current diff and apply
      -f, --force allow adding otherwise ignored files
      -u, --update update tracked files
      --renormalize renormalize EOL of tracked files (implies -u)
      -N, --intent-to-add record only the fact that the path will be added later
      -A, --all add changes from all tracked and untracked files
      --ignore-removal ignore paths removed in the working tree (same as --no
    -all)
      --refresh don't add, only refresh the index
      --ignore-errors just skip files which cannot be added because of
    errors
    --ignore-missing check if - even missing - files are ignored in dry run
      --sparse allow updating entries outside of the sparse-checkout
    cone
      --chmod (+|-)x override the executable bit of the listed files
      --pathspec-from-file <file> read pathspec from file
      --pathspec-file-nul with --pathspec-from-file, pathspec elements are
    separated with NUL character
```

---

Xem tiep: [Git basic](./git-basic.md)

# GIT COMMANDS

- ## Git Config

> Kiem tra va lay thong tin cau hinh

```bash
   # Liet ke thong tin cau hinh bao gom path
   $ git config --list --show-origin

   # Liet ke thong tin cau hinh khong bao gom path
   $ git config --list

   # Lay thong tin cau hinh bang thuoc tinh
   $ git config user.name
   $ git config user.email

   # Kiem tra Git dang ap dung cau hinh nao, Quan sat duong dan path de xem File cau hinh nao
   $ git config --show-origin user.name
```

> Thiet lap cau hinh

```bash
  # Thiet lap ten va email, editor, branch default cho Git
  $ git config --global user.name "username"
  $ git config --global user.email "email@gmail.com"
  $ git config --global core.editor "nano"
  $ git config --global init.defaultBranch "main"
```

- [Xem Cau Hinh Git](./git-setup.md)

---

- ## Git commands

> Them vao Staging Area

```bash
# Them vao Staging "(danh dau Stage)" tat ca
$ git add .

# Them vao Staging file cu the
$ git add demo

# Them vao Staging file co duoi cu the
$ git add *.sh

```

> Thuc hien Commit

```bash
# commit nhung file staged
$ git commit -m "first commit"

# Staged va commit file da tracked
$ git commit -am "Second commit"

# Sua lai mot commit
$ git commit --amned "Fix for second command"
```

> Kiem tra trang thai

```bash
# kiem tra trang thai
$ git status

# Kiem tra noi dung thay doi so voi noi dung staged truoc do
$ git diff [file-name]

# Kiem tra thay doi tu staged so voi last committed
$ git diff --staged [file-name]

# Kiem tra status voi --short
$ git status -s
```

> Staged & Commit thay doi

```bash
# Staged cac thay doi cho file cu the
$ git add filename

# Staged toan bo cac thay doi
$ git add .

# commit cac thay doi
$ git commit

# Commit voi noi dung diff trong Editor
$ git commit -v

# commit voi message
$ git commit -m "messsage"

# commit bo qua staged
$ git commit -a -m "message"
```

> Remove file va Remoe cached

```bash
# Remmove file bang lenh Git, ap dung cho file Tracked
$ git rm filename

# Remove voi matching pattern
$ git rm /\*.log

# Remove file voi --force
$ git rm -f filename

# Remove file ra khoi vung Staged khi da committed
$ git rm --cache filenamme

# Remmove file ra khoi Staged neu chua commit
$ git restore --staged filename
```

- [Git basic phan 2](./git-basic-2.md)

# GIT IGNORE

Git ignore noi de hieu la bo qua nhung phan ban khong muon Git theo doi hoac tu dong them vao cac file khong mong muon.
Thuong thi khi tao mot kho luu tru repository cuc bo bang `git init` mac dinh se khong co git ignore, neu nhu sao chep tu mot kho luu tru co san bang `git clone` thuong git ignore se co san trong kho luu tru.

Ten cua file Git ignore la `.gitignore`, gia su trong Working Tree ta co file `gitignore` voi noi dung;

```bash
$ cat .gitignore
*.[oa]
*~
```

Output cho ta biet 2 dieu

- **.[oa] :** Git bo qua cac doi tuong co duoi la `.a` hoac `.o`, su dung `pattern` de co the loc file theo yeu cau.
- **\*~ :** Git bo qua cac doi tuong ket thuc la `~`. dau `~` thuong thay trong cac `log`, `tmp`, cac file tam hoac cac thu muc `pid`.

Thuong trong qua trinh bien dich ma nguon hay build du an se phat sinh mot so file/ folder, dung `pattern` de ignore nhung file do.

```zsh
# Tao va them noi dung cho .gitignore tai vi tri goc cua Working Directory
$ cat > .gitignore << DOC
heredoc> *.[oa]
heredoc> *~
heredoc> /tmp/
heredoc>
heredoc> # Include file .env.example
heredoc> !.env.example
heredoc> DOC
```

Khi bat dau voi mot kho luu tru, viec tao `.gitignore` de bo qua nhung file khong mong muon la dieu nen lam dau tien, dieu nay se tranh viec vo tinh dua cac file co thong tin nhay vao vao commit cua Git.

##### Mot so quy tac ma `.gitignore` thuc thi

- Cac dong trong hoac dong bat dau bang # se duoc gitignore bo qua
- Cac `glob pattern` tieu chuam se hoat dong va duoc ap dung de quy cho moi cap do trong Working Deirectory
- Co the bat dau hoac ket thuc `pattern` la `/` de tranh de quy. `/pattern` hoac `pattern/`
- Co the phu dinh 1 `pattern` bang dau cham than `!`

`Glob patten` cung giong nhu bieu thuc chinh quy `regular expressions` ma cac shell hay trong ngon ngu lap trinh su dung. dau hoa thi `*` dai dien cho khong hoac la nhieu ky tu, `+` toi thieu la 1 hoac nhieu, [abc] 1 trong 3 ky tu, hoac `a` hoac `b` hoac `c`. `?` khop voi 1 ky tu don. Glob pattern no cunng tuong dong voi `wildcard` trong shell.

```text
a/**/z  : khop voi cac mau a//z, a/b/z, a/b/c/d/z
[abc]   : hoac a hoac b hoac c
a?f    : khop acf, adf. khong khop abcf, abcdef. Giua a va f chi duoc khop 1 ky tu don duy nhat
```

```text
# Bo qua tat ca file co duoi .a
*.a

# Bo qua cac file lib, nhung lib.a van tracking
!lib.a

# Chi bo qua file TOTO o vi tri hien tai .gitignore dang dung, khong lay sub dir cua subdir/TODO
/TODO

# Bo qua tat ca files trong bat ky folder nao ten build
build/

# Bo qua tat ca file co duoi la .txt trong foler doc, nhung doc/sub-folder/*.txt khong duoc bo qua
doc/*.txt

# BO qua tat cac cac files co duoi la .pdf trong folder doc va cac sub-folder cua no
doc/**/*.pdf
```

##### Luu y:

```text
    .gitignore se tac dong den cac doi tuong tinh tu vi tri ma no dang dung trong Working Directory, moi doi tuong thuoc cap cha se khong bi anh huong boi git ignore.

    Working tree
        |_ project_1
        |     |_ node_modules/
        |     |_ src/
        |     |_ .gitignore
        |
        |_ project_2
        |     |_ node_modules/
        |     |_ src/
        |     |_ TODO
        |     |_ .gitignore
        |
        |_ TODO
        |_ .gitignore

    Working directory hien tai voi 3 file .gitignore, tai vi tri cua moi .gitignore no chi tac dong den cac doi tuong cung cap hoac cap duoi no.

    Doi voi cac pattern thong thuong nhu /pattern hay pattern/ co nghia la khop mau chi dinh. Neu dung Glob pattern thi no de quy cho tat cac cac cap duoi neu khop pattern.

    project/
    ├── app.log
    ├── src/
    │   ├── debug.log
    │   └── test/
    │       └── error.log
    └── docs/
    |   └── build.log
    |
    |_ .gitignore

    # Bo qua tat ca pattern la .log, dung glob pattern de quy tat cac cap
    *.log

```

Trong thuc te, .gitignore co the duoc dat tai nhieu vi tri cap do khac nhau trong Working Tree, co the tan dung no de thuc hien cac yeu cau theo doi hoac khong theo doi nhung file mang tinh chat thong tin nhay cam hoac nhung file khong can thiet trong kho luu tru.

Tham khao: https://github.com/github/gitignore
Hoac dung `man gitignore` de doc huong dan su dung chi tiet

```bash
$ man gitignore
```

- [README](./README.md)
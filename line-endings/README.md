# line endings (CR & LF terminators)

common line-ending related issues, how to fix and avoid them.

## what are line terminators?

computers need to know when to start a new line, but the characters used to represent this can vary between platforms. this causes compatibility issues and unforeseen side effects, such as giant `git diff`s with no apparent change.

there are 2 control characters that represent line endings
- carriage return
  - aka `CR` `\r` `^M` `0x0d`
  - represents a cursor movement back to column 0
- line feed
  - aka `LF` `\n` `$` `0x0a`
  - represents a cursor movement directly downward

windows uses CR + LF to represent line-endings

any unix-like operating operating system (linux, \*BSD, macOS) represents line-endings with a single LF

## how to check line-endings

the `file` command will explicitly state `CRLF` endings; `LF` is implicit.
```shell
$ file lf.txt
lf.txt: ASCII text

$ file crlf.txt
crlf.txt: ASCII text, with CRLF line terminators
```

use `cat` with the `-v` or `-e` option
- `^M`=`CR`
- `$`=`LF`
```shell
$ cat -v crlf.txt # hides LF
never gonna give you up^M
never gonna let you down^M

$ cat -e crlf.txt # shows LF
never gonna give you up^M$
never gonna let you down^M$
```

## how to fix line-endings

### for one-off files...
use a tool like
- `dos2unix` / `unix2dos`
- `vim` `sed` `tr` etc...

most reliable is probably `dos2unix` (may require install)
```shell
$ dos2unix crlf.txt # convert to LF
$ unix2dos lf.txt   # convert to CRLF
```

some other ways
```shell
$ sed 's/\r$//' crlf.txt > lf.txt
$ tr -d '\r' < crlf.txt > lf.txt
```

### to configure git (+repos)

configure git locally to use to `LF` endings
```shell
git config --global core.autocrlf true
```

to configure line endings per-project...
create a `.gitattributes` file in project root dir
```shell
* text=auto
```

i recommend starting with [a template](https://github.com/alexkaratarakis/gitattributes)

to change endings in an EXISTING project:
```shell
# save files before changing
$ git add . -u
$ git commit -m "Saving files before refreshing line endings"

# renormalize endings (make sure run from project root)
$ git add --renormalize .

# check and commit
$ git status
$ git commit -m "normalize line endings"
```

## relevant links
- [gitattributes templates](https://github.com/alexkaratarakis/gitattributes)
- [github guide to line endings](https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings)


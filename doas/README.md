# doas

## video versions
- [youtube](https://www.youtube.com/watch?v=Tf4N0fjVjA4&t=105s)
- [odysee](https://odysee.com/@jediascode:9/doas:6)

## abstract
- `sudo` is a large tool with a number of past vulnerabilities, likely to have more.
  - see: [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156)
- `doas` has the functionality we need with much less code.
  - developed by Ted Unangst for OpenBSD

## install and configure
install doas from slicer69's github port
```
git clone https://github.com/slicer69/doas
# install dependencies based on your platform
make
sudo make install
make clean
```

configure `doas` config `/usr/local/etc/doas.conf`
```
permit youruser
# no password if you'd like
permit nopass youruser
```

read all the options at `man doas.conf`

disable `sudo`
```
doas visudo
# comment/delete all lines that privelege users
```

## links referenced
- [sudo project](https://www.sudo.ws/about/intro/)
- [sudo github mirror](https://github.com/sudo-project/sudo)
- [CVE-2021-3156](https://nvd.nist.gov/vuln/detail/CVE-2021-3156)
- [doas wiki](https://en.wikipedia.org/wiki/Doas)
- [doas github port](https://github.com/slicer69/doas)
- [doas.conf openBSD manpage](https://man.openbsd.org/doas.conf)

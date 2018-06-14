FROM archlinux/base
LABEL lind "v0.9-alpha"
LABEL description "Lind NaCl Glibc Toolchain (Base)"
MAINTAINER Joey Pabalinas <joeypabalinas@gmail.com>

ADD ["https://raw.githubusercontent.com/Lind-Project/lind_project/master/docker/pkgs.tar.xz", "/"]

ENV PATH "/usr/lind_project/lind/repy/sdk/toolchain/linux_x86_glibc/bin:$PATH"
ENV PATH "/usr/lind_project/lind/repy/bin:$PATH"
ENV PATH "/usr/lind_project:$PATH"
ENV PATH "/root/.local/bin:$PATH"
ENV WORKON_HOME "/root/.virtualenvs"
ENV VIRTUALENVWRAPPER_PYTHON "/usr/bin/python2"
ENV VIRTUALENVWRAPPER_VIRTUALENV "/usr/bin/virtualenv2"
ENV LIND_BASE "/usr/lind_project"
ENV LIND_SRC "/usr/lind_project/lind"
ENV LIND_MONITOR "/usr/lind_project/reference_monitor"
ENV NACL_SDK_ROOT "/usr/lind_project/lind/repy/sdk"
ENV REPY_PATH "/usr/lind_project/lind/repy"
ENV PNACLPYTHON "/usr/bin/python2"
ENV PYTHON "/usr/bin/python2"
ENV LD_LIBRARY_PATH "/lib/glibc"

WORKDIR /
RUN ["/usr/bin/bsdtar", "xvf", "pkgs.tar.xz"]
RUN ["/usr/bin/pacman", "-Syu", "--noconfirm", "gawk", "inetutils", "procps-ng", "ruby"]
RUN ["/usr/bin/pacman", "-S", "--noconfirm", "base-devel", "w3m", \
    "git", "mercurial", "rsync", "make", "perl", "clang", "lynx", "ed", \
    "compiler-rt", "lib32-clang", "lib32-llvm", "lib32-llvm-libs", "vim", \
    "llvm", "llvm-libs", "openmp", "elfutils", "libelf", "gdb", "less", \
    "gnu-netcat", "zsh", "zsh-completions", "grml-zsh-config", "htop", \
    "ncurses", "gcc-libs", "lib32-gcc-libs", "gperf", "diffutils", \
    "gperftools", "texinfo", "fortune-mod", "bash-completion", "gnupg", \
    "screen", "python2", "python2-pip", "python2-setuptools", "p7zip", \
    "python2-virtualenv", "python-virtualenvwrapper", "pkgfile", "dhcpcd", \
    "iputils","python", "iproute2", "net-tools", "openresolv", "ranger", \
    "openssh", "subversion", "pacman-contrib", "arch-wiki-docs"]
RUN ["/usr/bin/pkgfile", "--update"]
WORKDIR /usr/bin/
RUN ["/usr/bin/ln",  "-Trsfv", "python2", "python"]
WORKDIR /root/build/
RUN ["/usr/bin/lesskey"]
RUN ["/usr/bin/pip2", "install", "--user", "-Ur", "requirements.txt"]
RUN ["/usr/bin/tic", "screen-256color-italic.terminfo"]

WORKDIR /root/build/terminfo-italics/
RUN ["/usr/bin/env", "EUID=1000", "/usr/bin/makepkg", "--noconfirm", "--skipchecksums", "--skippgpcheck", "-sir"]
WORKDIR /root/build/cower/
RUN ["/usr/bin/env", "EUID=1000", "/usr/bin/makepkg", "--noconfirm", "--skipchecksums", "--skippgpcheck", "-sir"]
WORKDIR /root/build/pacaur/
RUN ["/usr/bin/env", "EUID=1000", "/usr/bin/makepkg", "--noconfirm", "--skipchecksums", "--skippgpcheck", "-sir"]
WORKDIR /root/build/make-3.82/
RUN ["/usr/bin/env", "EUID=1000", "/usr/bin/makepkg", "--noconfirm", "--skipchecksums", "--skippgpcheck", "-sir"]
WORKDIR /root/build/texinfo-4.13/
RUN ["./configure", "--prefix=/root/.local"]
RUN ["/usr/bin/make", "install", "PREFIX=/root/.local"]

WORKDIR /usr/
RUN ["/usr/bin/git", "config", "--global", "user.name", "Lind"]
RUN ["/usr/bin/git", "config", "--global", "user.email", "wooo@weee.woah"]
RUN ["/usr/bin/git", "config", "--global", "core.excludesFile", "/root/.cvsignore"]
RUN ["/usr/bin/git", "clone", "--progress", "-j4", "https://github.com/Lind-Project/lind_project.git"]

WORKDIR /usr/lind_project/
RUN ["/usr/bin/mkdir", "-pv", "lind/repy/lib/glibc/"]
RUN ["/usr/bin/cp", "-av", "/root/build/tls", "lind/repy/lib/glibc/"]
RUN ["/usr/bin/rm", "-rf", "/root/build/", "/var/cache/pacman/pkg/"]

CMD ["/usr/bin/bash"]
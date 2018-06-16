# Build libc with debug info

本文使用環境為 64 bit Ubuntu 16.04

## Download source code

由 [The GNU C Library (glibc)](https://www.gnu.org/software/libc/) 官方網站下載 glibc source code，以 glibc 2.23 為例

下載 glibc 2.23 並解壓縮

```shell
wget https://ftp.gnu.org/gnu/libc/glibc-2.23.tar.gz
tar zxvf glibc-2.23.tar.gz
```

## Configure and build

進入 glibc 資料夾中並新增一個 build 的資料夾供編譯使用

```shell
cd glibc-2.23
mkdir build
```

進入 build 資料夾並設定編譯參數

- CFLAGS
    - debug 選項全開並盡量不要做優化
    - 可參考以下範例
- prefix
    - 編譯完檔案所放位置
    - 範例為放置家目錄下的 glibc 資料夾內

```shell
cd build
CFLAGS='-g3 -ggdb3 -gdwarf-4 -Og -Wno-error' ../configure --prefix=/home/`whoami`/glibc
```

編譯並安裝

```shell
make -j4
make install -j4
```

## Note

編譯 32 bit 版本的 glibc

- CC
    - gcc -m32
- CFLAGS
    - host=i686-linux-gnu
    - build=i686-linux-gnu

```CC='gcc -m32' CFLAGS='-g3 -ggdb3 -gdwarf-4 -Og -Wno-error --host=i686-linux-gnu --bulid=i686-linux-gnu' ../configure --prefix=/home/`whoami`/glibc```

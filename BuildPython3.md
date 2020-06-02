# Build Python 3

## Ubuntu 16.04 & Ubuntu 18.04

CTRL-ALT-T and ensure needed prerequisite packages are installed:

Ubuntu 16.04

```
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
```

Ubuntu 18.04

```
sudo apt-get install build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev zlib1g-dev libssl-dev openssl libgdbm-dev libgdbm-compat-dev liblzma-dev libreadline-dev libncursesw5-dev libffi-dev uuid-dev
```

Go to https://www.python.org/downloads/source/ and figure out the URL for the latest
Python 3 release, e.g. https://www.python.org/downloads/release/python-383/

Now determine the URL of the tarball, it might be:

https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz

Download it with curl:

```
cd ~/Downloads
sudo apt install curl
curl https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz -o python3.tgz
```

Unzip the file:

```
tar xvzf python3.tgz
```

CD into the new directory created e.g. `Python-3.8.3`:

```
cd Python-3.8.3
```

Configure it option 1:

```
./configure --enable-optimizations --enable-shared
```

Note that the `./configure` step suggests using the `--enable-optimizations` flag. Apparently this will make
Python run about 10% faster, but takes about 40 minutes to build since it forces running the tests.

The `--enabled-shared` option is needed for `mod_wsgi`.

Configure option 2 for local libraries (See StackOverflow below):

```
./configure --enable-shared --prefix=/usr/local LDFLAGS="-Wl,--rpath=/usr/local/lib"
./configure --enable-optimizations --enable-shared --prefix=/usr/local LDFLAGS="-Wl,--rpath=/usr/local/lib"
```

Build it - approx 2 mins (without the `--enable-optimizations` option):

```
make
```

Test it - approx 15 mins (redundant if you used `--enable-optimizations`):

```
make test
```

Install it:

```
sudo make install
```

Check version

```
python3.8 --version
```

### Debugging

#### python3: error while loading shared libraries: libpython3.6m.so.1.0: cannot open shared object file: No such file or directory

```
ldd /usr/local/bin/python3
```

Create a symbolic link to fix the problem:

```
sudo ln -s /usr/local/lib/libpython3.6m.so.1.0 /usr/lib/libpython3.6m.so.1.0
```

See compile time possibilities to stop this error in the first place:
https://stackoverflow.com/questions/7880454/python-executable-not-finding-libpython-shared-library

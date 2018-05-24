# Build Python 3

## Ubuntu 16.04

CTRL-ALT-T and ensure needed prerequisite packages are installed:
```
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
```

Go to https://www.python.org/downloads/source/ and figure out the URL for the latest
Python 3 release, e.g. https://www.python.org/downloads/release/python-365/

Now determine the URL of the tarball, it might be:

https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz

Download it with curl:
```
sudo apt install curl
curl https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz -o python3.tgz
```

Unzip the file:
```
tar xvzf python3.tgz
```

CD into the new directory created e.g. `Python-3.6.5`:
```
cd Python-3.6.5
```

Configure it:
```
./configure
```
Note that the `./configure` step suggests using the `--enable-optimizations` flag. Apparently this will make
Python run about 10% faster, but takes about 40 minutes to build since it forces running the tests.

Build it - approx 2 mins:
```
make
```

Test it - approx 15 mins:
```
make test
```

Install it:
```
sudo make install
```

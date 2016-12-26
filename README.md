Minsky dev steps
================

This was my attempt to do dev on Minsky.

Went through Minsky's .travis.yml & installed and built everything

Setting up checkout
-------------------

```
git clone https://github.com/highperformancecoder/minsky.git
cd minsky
git remote add upstream https://github.com/highperformancecoder/minsky.git
git remote set-url origin https://github.com/brantlk/minsky.git
git remote set-url --push origin git@github.com:brantlk/minsky.git
git fetch --all
```

When re-clone:

```
cd /vagrant/minsky
git clone https://github.com/highperformancecoder/ecolab.git
pushd ecolab
git submodule init
git submodule update
make install
popd

make DEBUG=1
Xvfb :1 &>/dev/null &
export DISPLAY=:1
export MINSKY_TEST_DATABASE_PARAMS=$HOME/.testDatabase
echo "testEq.mky" >$MINSKY_TEST_DATABASE_PARAMS

sudo -u postgres createuser --superuser $USER
sudo -u postgres psql
  \password vagrant
  (don't set a password)
sudo -u postgres createdb $USER

psql -U $USER <server/minskyPG.sql
echo "postgresql://dbname=$USER user=$USER password=">>$MINSKY_TEST_DATABASE_PARAMS
make AEGIS=1 sure
```


When restart:

```
cd /vagrant/minsky/ecolab
make install
cd /vagrant/minsky
export MINSKY_TEST_DATABASE_PARAMS=$HOME/.testDatabase
echo "testEq.mky" >$MINSKY_TEST_DATABASE_PARAMS

sudo -u postgres createuser --superuser $USER
sudo -u postgres psql
  \password vagrant
  (don't set a password)
sudo -u postgres createdb $USER

psql -U $USER <server/minskyPG.sql
echo "postgresql://dbname=$USER user=$USER password=">>$MINSKY_TEST_DATABASE_PARAMS

gui-tk/minsky
```


Open a test ssh:

```
vagrant ssh

Xvfb :1 &>/dev/null &
export DISPLAY=:1
cd /vagrant/minsky
make AEGIS=1 sure
```

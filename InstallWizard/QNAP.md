# Python and PIP on Qnap

For Python 2.7 and Pip on QNAP perform the following steps,

1) Install the Python 2.7.12.1 package from the Qnap App Store

2) Log in to your NAS via ssh

3) Enter the command below

```
export PATH=/opt/QPython2/bin:$PATH
```
4) Check the correct version of Python is installed and active using
```
python --version
```
This should return
```
python 2.7.12.1
```
5) Install Pip using
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
```
6) Install Flexget using
```
Pip install flexget
```
7) Create the directory below and add your config.yml
```
/root/.flexget
```
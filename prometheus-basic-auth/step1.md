Prometheus takes passwords hashed with bcrypt. To validate the password,
it does not need to know exactly your password. Instead, it needs a "hash" of
the password, which will be compared to the password you provide to your
Prometheus server.

This way of working means that no clear text password is stored in the file. It
also means that you need to provide a hashed version of the password, which is
an step that can be done in multiple ways.


## Pre-requisites

To generate a hashed password, we will use python3-bcrypt.

Let's install it by running `apt install python3-bcrypt`{{execute}}

There are other ways to do that, we had to pick one way. Python is already
present on most systems, so that seems like a great way to start.

## Generate the password

Here is a one-liner which will prompt for a password and store it:

`clear;python3 -c 'import getpass;import bcrypt;print(bcrypt.hashpw(getpass.getpass("password: ").encode("utf-8"), bcrypt.gensalt()).decode())'`{{execute}}

To make that easier to read, you can also paste this into a file, called
`bcrypt.py`. To do so, type the following commands:

cat << EOF > gen-pass.py
import getpass
import bcrypt

password = getpass.getpass("password: ")
hashed_password = bcrypt.hashpw(password.encode("utf-8"), bcrypt.gensalt())
print(hashed_password.decode())
EOF
```{{execute}}

That has generated a file, `gen-pass.py`{{open}}, which can be called to generate a
password.

Now, launch the script and type your password. You should get in return a hashed
version of the password: `python3 gen-pass.py`{{execute}}

That will prompt you for a password:
```
password:
$2b$12$hNf2lSsxfm0.i4a.1kVpSOVyBCfIB51VRjgBUyv6kdnyTlgWj81Ay
```

In this exemple, I used "test" as password.

Save that password somewhere, we will use it in the next steps!

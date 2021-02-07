Let's download and prepare Prometheus. We will use Prometheus 2.24.1, which is
the first release to have basic authentication support.

# Download Prometheus

```
$ wget https://github.com/prometheus/prometheus/releases/download/v2.24.1/prometheus-2.24.1.linux-amd64.tar.gz
$ tar xf prometheus-2.24.1.linux-amd64.tar.gz
$ cd prometheus-2.24.1.linux-amd64
```

You should now see a bunch of files:

```
$ ls
console_libraries  consoles  LICENSE  NOTICE  prometheus  prometheus.yml promtool
```

## Create web.yml

Let's create a web.yml file ([documentation](https://prometheus.io/docs/prometheus/latest/configuration/https/)):

```
$ cat << 'EOF' > web.yml
basic_auth_users:
    alice: $2b$12$hNf2lSsxfm0.i4a.1kVpSOVyBCfIB51VRjgBUyv6kdnyTlgWj81Ay
EOF
```

Notes:
- We use `'EOF'` in this exemple to avoid variable expansion. Without this, the
  hashed password would be truncated.
- Spacing is important.
- The username is `alice` and the password is copied from the previous step.

## Validate web.yml

You can validate that file with `promtool check web-config`:

```
$ ./promtool check web-config web.yml
web.yml SUCCESS
```

## Start Prometheus

You can now launch Prometheus, with the web.yml file:

```
$ ./prometheus --web.config.file=web.yml
```

Prometheus should now be running!

You can try to login to your prometheus server at
https://[[HOST_SUBDOMAIN]]-9090-[[KATACODA_HOST]].environments.katacoda.com/

It should prompt you for your username and password.

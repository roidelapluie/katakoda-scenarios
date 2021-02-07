# Test the setup!

You can now test the setup. To do so, we will use curl in the second terminal.

Without authentication:

```
$ curl 127.0.0.1:9090
Unauthorized
```

With a password:

```
$ curl -su alice 127.0.0.1:9090/api/v1/query?query=up|jq
Enter host password for user 'alice':
{
  "status": "success",
  "data": {
    "resultType": "vector",
    "result": [
      {
        "metric": {
          "__name__": "up",
          "instance": "localhost:9090",
          "job": "prometheus"
        },
        "value": [
          1612711439.747,
          "0"
        ]
      }
    ]
  }
}
```

If you enter a wrong user or password, you should get an `Unauthorized` message:

```
$ curl -su bob 127.0.0.1:9090/api/v1/query?query=up
Enter host password for user 'bob':
Unauthorized
```

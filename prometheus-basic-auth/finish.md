# Conclusion

This was a quick demonstration about the basic authentication features of
Prometheus.

That the web.yml file can be changed on the flight, which means
that if you add users or change passwords in the file, you do not need to
restart or reload Prometheus. Changes will be taken in consideration in the next
request.

This method will expose the passwords in clear text over the network, but
Prometheus also supports TLS and client-certificate authentication, if you want
another level of security.

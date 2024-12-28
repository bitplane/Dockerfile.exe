# Self executing Dockerfile

`awk` runs its own params and can access its second param, which means it
can be used to make a self-executing Dockerfile:

```docker
#!/bin/awk BEGIN { system("t=$(mktemp -d); cat " ARGV[1] " > $t/Dockerfile; cd $t; docker run --rm $(docker build -q .); rm -rf $t") }
FROM alpine

ENTRYPOINT ["sh", "-c", "echo hello world"]
```

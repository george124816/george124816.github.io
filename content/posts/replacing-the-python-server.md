---
date: '2026-03-14T19:05:01-05:00'
draft: false
title: 'Replacing the Python Server'
summary: 'Every time that need to serve a simple files I use the famous 
`python -m http.server 4000`, today I questioning myself about to use python because its a language that I never used in my life, and a simple project came up, why not use my own project to serve my files in golang?'
---

Every time that need to serve a simple files I use the famous 
`python -m http.server 4000`, today I questioning myself about to use python because its a language that I never used in my life, and a simple project came up, why not use my own project to serve my files in golang?

I created a simple file that use a few packages from stdlib

```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"os"
	"strconv"
)

var directory string
var defaultDirectory string = "."

var port int
var defaultPort int = 8000

func main() {
	port = defaultPort
	if s := os.Getenv("PORT"); s != "" {
		if p, err := strconv.Atoi(s); err == nil {
			port = p
		}
	}

	directory = defaultDirectory
	if s := os.Getenv("DIR"); s != "" {
		directory = s
	}

	log.Printf(`serving directory "%s" on port "%d"`, directory, port)
	log.Fatal(http.ListenAndServe(fmt.Sprintf(":%d", port), http.FileServer(http.Dir(directory))))
}
```

and how to use this easily? I send to my github and with a few commands I can install and use this

```sh
go install github.com/george124816/fileserver@latest
PORT=8000 DIR=/tmp/ fileserver
```

refs: https://github.com/george124816/fileserver

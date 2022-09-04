```
$ nx init
$ tree -L 1
.
├── README.md
├── node_modules
├── nx.json
├── package-lock.json
└── package.json
```

```
package main

import (
	"fmt"
	"os"
)

func check(e error) {
	if e != nil {
		panic(e)
	}
}

func main() {
	fmt.Println("Hello, World!")
	dat, err := os.ReadFile("src/cow.txt")
	check(err)
	fmt.Print(string(dat))
}
```

```
 _____
< moo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

```
{
  "root": "packages/cli",
  "sourceRoot": "packages/cli/src",
  "projectType": "application",
  "targets": {
    "build": {
      "executor": "nx:run-commands",
      "options": {
        "command": "go build -o='../../dist/packages/cli/' ./src/ascii.go",
        "cwd": "apps/cli"
      }
    },
    "serve": {
      "executor": "nx:run-commands",
      "options": {
        "command": "go run ./src/ascii.go",
        "cwd": "apps/cli"
      }
    }
  }
}

```

```
{
  "$schema": "./node_modules/nx/schemas/workspace-schema.json",
  "version": 2,
  "projects": {
    "cli": "apps/cli"
  }
}
```

```
nx run [project][:target][:configuration] [_..]
```

`single-module`
root に一つだけ`go.mod`がある

`multi-module`
各ディレクトリに go.mod があるじょうたい

`workspace mode`

```
$ npx nx run cli:serve

> nx run cli:serve

Hello, World!
 _____
< moo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

 ———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 >  NX   Successfully ran target serve for project cli
```

```
$ go work init

$ go work use -r .

$ cat go.work
go 1.19

use ./apps/cli
```

```
{
  "root": "packages/ascii",
  "sourceRoot": "packages/ascii/assets",
  "projectType": "library"
}
```

```
$ npx nx run cli:serve

> nx run cli:serve

Hello, World!
 _____
< moo! >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

 ———————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

 >  NX   Successfully ran target serve for project cli

```

```
$ nx affected --target=build

 >  NX   Affected criteria defaulted to --base=main --head=HEAD

 >  NX   Successfully ran target build for 0 projects (1ms)
```

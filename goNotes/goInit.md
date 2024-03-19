# Learning Go with Vim


## Init a module

After creating a project directory, you then initialize a module for this directory. It will 
keep track of the packages (as well as their versions) you use.


`go mod init [url or module name]`


moduleName works just fine for messing around, but if you want other people to use it, must be 
in url. Easiest practice would be the github link to your project.


Can have multiple of these in one project. Let's say proj has moduleA and moduleB. There would 
be 2 directories for both of these. In each of those dirs, there would be a seperate go.mod 
file. There would be a go.mod file for the over all file as well.

## Importing module

`import "module-name/orDir"`

Can also be structured like

```
import (
	"fmt"
	"net/http"
)
```

## important command for local testing

If we don't have a project module available on a url, import statement won't work
So what we do is we go to the project that is calling the module (which is unavaialable)
and then in that directory we do 

`replace [url] => [localPath]`

This has other uses such as:

1. testing experimental changes
2. working with forks or private repos
3. offline dev
4. dependency override



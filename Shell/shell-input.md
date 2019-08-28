#Brief
The shell command and any arguments to that command appear as *numbered* shell variables: `$0` has the string value of the command itself, something like `script`, `./script`, `/home/user/bin/script` or whatever. Any arguments appear as `"$1"`, `"$2"`, `"$3"` and so on. The count of arguments is in the shell variable `"$#"`. 


#Command
```shell
$ cat myscript
#!/bin/bash
echo "$#"
echo "$0"
echo "First arg: $1"
echo "Second arg: $2"
$ ./myscript hello world
2
./myscript.sh
First arg: hello
Second arg: world
```
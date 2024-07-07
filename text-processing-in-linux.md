# REDIRECT
### stdin -> means standard input code is 0
### stdout -> means standard output code is 1
### stderr -> means standard errors code is 2

## To wrtite all erros that occures while running a commands in a specified file
```
sudo bash run.sh 2 > errors.txt 
```

here `run.sh` is the bash script we want to run and `2` is the code for `stderr` so whatever errors occured while running the bash script will be written in the file  `errors.txt`

## to wrtie all logs into a file (boath errors and standard logs)

``` 
sudo bash run.sh >> logs.txt 2>&1 
```
this will write all the logs to `logs.txt` file.

## USe of input redirect
 `<` is used for input redirect 

 ```
 cat < logs.txt
```

though cat logs.txt will return similar result but in some cases input redirects are rewuired like wc command

```
wc -l logs.txt 
```
will return <`no of lines` > `logs.txt` 
but 
```
wc -l <logs.txt
```
will return only the number of lines.  this might be useful in shell scripting


# AWK command
used for  pattern base text processing like csv -> comma separated value

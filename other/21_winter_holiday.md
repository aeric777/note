# 21-Winter-Holiday
> 2021.11.22

## **missing-semester 课程笔记**

### 学习资料
[Bilibili视频讲解](https://www.bilibili.com/video/BV1x7411H7wa) 、 [MIT官方网站](https://missing.csail.mit.edu/) 、 [Github项目](https://github.com/missing-semester/missing-semester) 、 参考[同步exercise笔记](https://www.zybuluo.com/aeric777/note/1775177)


### **Lesson-1 (Course overview + the shell)**
**知识点**
>- command-line
>- Shell on Linux:
1.Basic operation: cd pwd which ls cp mkdir rm mv  
2.Connecting program:  < 、 > 、 <<  、>> 、 |


### **Lesson-2 (Shell Tools and Scripting)**
**知识点**
> - assign value to the variable  : `$`
> - define function with Bash script , `source` before you use the function
> - reserved  words will be replaced directly(`$0`(file name) , `$1~$9`(each argument) , `#?`(if an error happened), `$_`(last argument), `&&`(pid), `&#`(number od argument))
> - `!!` , `;`
> - logical operator : `||` , `&&` , `-ne`(not equal)

```
   grep foobar "$file" > /dev/null 2> /dev/null
   "redirect STDOUT and STDERR to a null register.
```
> - `?` , `*`
> - `convert`
> - using `{}`
> - `shellcheck`
> - `find`

```
eric@eric-VirtualBox:~$find . -name src -type d
```

####**Bash Shell脚本运行**

- 可使用 `source` (~~原因不明~~，problem solved)
> 
**What is the difference between source script.sh and ./script.sh?**
　　In both cases the script.sh will be read and executed in a bash session, the difference lies in which session is running the commands.
　　For `source` the commands are **executed in your current bash session** and thus any changes made to the current environment, like changing directories or defining functions will persist in the current session once the source command finishes executing.
　　When **running the script standalone** like `./script.sh`, your current bash session **starts a new instance of bash** that will run the commands in script.sh. Thus, if script.sh changes directories, the new bash instance will change directories but once it exits and returns control to the parent bash session, the parent session will remain in the same place. 
　　Similarly, if script.sh **defines a function that you want to access in your terminal**, you need to `source` it for it to be defined in your current bash session. Otherwise, if you run it, the new bash process will be the one to process the function definition instead of your current shell.
>

- 路径法
  1. 相对路径（移动到对应文件夹后） `./name` 运行脚本
  2.  `./` 换为 `绝对路径`

- 执行脚本前确定是否有执行权限 `x`
- 定义的函数经过 `source` 后可在任意位置运行


### **Lesson-3 (Editors - Vim)**
**知识点**
- **Remember that you can always find all the KEY command in vimtutor.**
- Modes(normal, insert, visual-line,visual-block, command-line)
- useful command(`:q`,`:w`,`:qa`,`:tabnew`,`:sp`)
- `u` means **undo**  ; `^r` means **redo**
- `x`(`r`) delete(replace) one character in normal mode
- `R` to replace more character without erasing those character until you type the new character.(Which means every typed character deletes an existing character)
- `y` for copy(yank) the chosen character; `yy` to copy the whole line
- `d` for delete the chosen character; `dd` to delete the whole line
- note that the `d` and `y` can be combine with other key like `dw`(delete the word ) `yw` (copy the word)
- `shift+v`(visual by line), `^v`(visual by block)
- combination of `[count]command`
- `i` of inside(`di[` to delete the context inside the []) and  `a` for  around
- `/`(forward slash) for search and move to specific position 
- `.` repeat the command you have done before
- `gg`to the top; `G`to the bottom; `[number] G`to the specific line
- `ctrl-g`display your current location in the file.
- `/`to search word the press`[Enter]`, your cursor will jump to that location. If you want to search for the same word again , **type`n`or`N`**.(Note that you can always use `?` to do the same thing but in a opposite direction)
- `Ctrl-o`goes to the backward place that you came from ;and `Ctrl-i`to goes to the forward place that you came from.
- Type `%` to move to the matched **bracket**`(){}[]`
- **Important!** `:s/old/new`change `old`to `new`,while `:s/old/new/g`change`old` in the whole line.What's more, `:#,#s/old/new`change in a range between two line;`:%s/old/new/g`change ine whole file;`:%s/old/new/gc`give you a prompt whether to substitute or not.
- `:![command]` to use an external command 
- press `v` into `visual Mode` then `motion  :w FILENAME `to saves the Visually selected lines in file `FILENAME`.
- you can also use `:r` to merge file into your current position
- press `ctrl-d`to show what command you can use when you forget part of a command 


### **Lesson-4 (Data Wrangling)**
    using `|` as an important operator 
**知识点**
####**Regular Expression**(normally deal with **text**)
- use the [Website](https://regex101.com/) to check your Regex.
- Note that all the Regex is **greedy match** in default. But you can always use `?`after a specific regex to make it an **ungreedy match**
- The Regex work **per line**.
- `.` match any possible single character.
- `[pattern] *`means zero or more character of that pattern.
```
Note that if you use `.*[expression]` to match any possible character before target[expression] , it also match the `[expression]` itself
```
- `[argument1 argument2.....]` match one argument that met first
- `(argument1 argument2.....)`require a fully match

####**Useful_Function**
- `wc` -  initials of word counter
- `sort` take arguments and then sort them
- `uniq` print the unique argument(`uniq -c` print the repeat time at the same time)
- `awk` - kind of program language that deal with stream
- `sd`
- `bc` -initials of **Berkeley calculator**,also operate calculation with stream.

Input:
```
echo "1+2" | bc -l
```
Output:
```
3
```
- `xargs` transfer output into arguments



### **Lesson-5 (Command-line Environment)**
**知识点**
####`alias`
```
alias alias_name="command_to_alias arg1 arg2"
```
　　Note that `alias` takes only **one argument**.
　　
####Job Control
　　Your bash shell is using a UNIX communication mechanism called *signal*.**When a process receives a signal it stops its execution, deals with the signal and potentially changes the flow of execution based on the information that the signal delivered.**
- `ctrl-c` represent the `SIGINT`signal
- `ctrl-\` represent the `SIGQUIT`signal
- `ctrl-z` represent the `SIGSTOP`signal
- `fg`,`bg`command continue a paused porgram in the foreground or in the background.
- `jobs`show you all the running or paused program 
-  the `&` suffix in a command will run the command in the background
- `nohup` (a wrapper to ignore SIGHUP)
- `kill` kill a program 

　　
####Terminal Multiplexers

#####Sessions
- `tmux `starts a new session
- `tmux new -s [NAME]`starts a new program with specific [NAME]
- `tmux ls`list all your current sessions
- Within a `tmux`,using `<c-b> d`to detach the current session 
- `tmux a`attaches the last session,you can always use `-t`flag to specify which to attach

#####Windows(Within `tmux`)
- `<c-b> c`create a new window,use `<c-d>`to close this window
- `<c-b> [Number]`goto the [Number] window
- `<c-b> p`goto the previous window
- `<c-b> n`goto the next window
- `<c-b> ,`rename the current window
- `<c-b> w`list all the current window

#####Panes(like vim `splits`)
- `<c-b> "`Split the current pane horizontally
- `<c-b> %`Split the current pane vertically
- `<c-b> [arrow-key]`Move to the pane in the **specified direction**
- `<c-b> `Toggle zoom for the current pane
- `<c-b> [`Start scrollback.
- `<c-b> [space]`Cycle through different pane arrangements.

####Dotfiles
configure your **Dotfiles**
- `bash` - `~/.bashrc`, `~/.bash_profile`
- `git` - `~/.gitconfig`
- `vim` - `~/.vimrc` and the `~/.vim` folder
-  `ssh` - `~/.ssh/config`
-  `tmux` - `~/.tmux.conf`

####Remote Machines


### **Lesson-6 (version-control)**
**知识点**
####Git's data model
　　[Watch here](https://github.com/missing-semester/missing-semester/blob/master/_2020/version-control.md)for more details!
　　Git models the history of a collection of files and folders within some top-level directory as a series of snapshots.
　　In Git terminology, file is called **"blob"**, and directory is called **"tree"** which maps the name of blobs and other tree. 
　　

#####pseudo code of Git
```
// a file is a bunch of bytes
type blob = array<byte>

// a directory contains named files and directories
type tree = map<string, tree | blob>

// a commit has parents, metadata, and the top-level tree
type commit = struct {
    parent: array<commit>
    author: string
    message: string
    snapshot: tree
}
```
```
type object = blob | tree | commit  //An "object" is a blob, tree, or commit
objects = map<string, object>

//In Git data store, all objects are content-addressed by their SHA-1 hash.
def store(object):
    id = sha1(object)
    objects[id] = object

def load(id):
    return objects[id]
```

### **Lesson-7 (Debugging and Profiling)**
The Debug skill is basically all about python.

#### Build in system
　　Using `make` file.

### **Lesson-8 (Meta programming)**
**知识点**
#### Test
(PS:This lesson is almost all about Python.)


### **Lesson-9 (Security and Cryptography)**
**知识点**
#### Calculate the Entropy
　　The entropy is equal to `log_2(# of possibilities)`. For example: a fair coin flip gives 1 bit of entropy. A dice roll (of a 6-sided die) has ~2.58 bits of entropy.
#### Hash Function
　　A **cryptographic hash** function maps data of arbitrary size to a **fixed size**, and has some special properties. 
　　An example of a hash function is `SHA1`, which is used in Git. It maps arbitrary-sized inputs to **160-bit outputs** (which can be represented as **40 hexadecimal characters**). Use `sha1sum` command to check. 
　　Note that hash function is a one way usage function.


#### Key derivation functions(KDFs)
　　Usually, KDFs are deliberately **slow**, in order to slow down offline brute-force attacks.


#### Symmetric cryptography
　　Basic functionality:
```
openssl aes-256-cbc -salt -in {input filename} -out {output filename}
openssl aes-256-cbc -d -in {input filename} -out {output filename}
```
```
//Use as openssl
keygen() -> key  (this function is randomized)

encrypt(plaintext: array<byte>, key) -> array<byte>  (the ciphertext)
decrypt(ciphertext: array<byte>, key) -> array<byte>  (the plaintext)
//You can decrypt the ciphertext into plaintext only if you have the key which is generated randomly in your local machine.
//btw,You can also use KDFs as your keygen() function.
```
```
decrypt(encrypt(m, k), k) = m       //which is obvious.
```


#### Asymmetric cryptography
```
//Use in ssh, public email service

keygen() -> (public key, private key)  (this function is randomized)
//generate a pair of keys
encrypt(plaintext: array<byte>, public key) -> array<byte>  (the ciphertext)
decrypt(ciphertext: array<byte>, private key) -> array<byte>  (the plaintext)

sign(message: array<byte>, private key) -> array<byte>  (the signature)
verify(message: array<byte>, signature: array<byte>, public key) -> bool    //whether or not the signature is valid
```

#### Key distribution for Asymmetric cryptography
　　Asymmetric-key cryptography is wonderful, but it has a big challenge of **distributing public key**/ mapping public key to real -world identities.
　　There are many solutions base on different strategies.


#### Details of the work flow in SSH
　　In use, once the server knows the client's **public key** (stored in the `.ssh/authorized_keys file`), a connecting client can prove its identity using asymmetric signatures. 
　　This is done through **challenge-response**. At a high level, the server picks a random number and sends it to the client. The client then signs this message and **sends the signature back to the server**, which checks the signature against the public key on record. This effectively proves that the client is in possession of the private key corresponding to the public key that's in the server's `.ssh/authorized_keys` file, so the server can allow the client to log in.

### **Lesson-10 (Potpourri)**
　　See more detail in this [website](https://github.com/missing-semester/missing-semester/blob/master/_2020/potpourri.md). 

### **Lesson-11 (Q&A)**
　　See more detail in this [website](https://github.com/missing-semester/missing-semester/blob/master/_2020/qa.md). 
　　
　　**When do I use Python versus a Bash scripts versus some other language?**
　　Therefore, for larger and/or more complex scripts we recommend using more mature scripting languages like Python or Ruby. For some small and simple action ,you can basically use bash script to finish it.
　　
　　**Should I apt-get install a python-whatever, or pip install whatever package?**
　　
　　
　　**Any more Vim tips?**

- Plugins - Take your time and explore the plugin landscape. There are a lot of great plugins that address some of vim's shortcomings or add new functionality that composes well with existing vim workflows. For this, good resources are VimAwesome and other programmers' dotfiles.
- Marks - In vim, you can set a mark doing m<X> for some letter X. You can then go back to that mark doing '<X>. This lets you quickly navigate to specific locations within a file or even across files.
- Navigation - `Ctrl+O` and `Ctrl+I` move you backward and forward respectively through your recently visited locations.
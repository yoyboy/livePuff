# livePuff

# Linux command

### 查看文件夹下有几个文件
```linux
ls | wc -w
```

### 删除后缀名为xxx的文件(可用正则筛选)
```linux
find . -name "xxx" | xargs rm -rf
```
#### 如 find . -name "\*\_aaa\_\*" , 筛选出文件名有aaa字段的文件, 再删除

### 查找目录下按具体时间过滤的文件
```linux
ls --full-time *_jpg_* | sed -n '/2019-07-02/p'
```
#### 查询在2019年7月2号被改动的jpg文件

### 查找目录下某文件的修改时间
```linux
ll | grep xxx
```

### 全局搜索
```linux
find / -name xx.xx
```
# git

### 使用git merge --squash合并代码(假设是将feature合并到master)
#### 切换到想要合并的分支(切换前确保开发分支已提交), 并拉取最新的代码
```git
git checkout master
git pull origin master:master
```
#### git合并
```
git merge --squash feature
```
#### 此时有冲突需手动解决冲突
```git
git status 查看有冲突的文件并解决冲突
git add ConflictFile 添加已解决冲突的文件
```
#### git提交, 推送
```git
git commit -m "merge feature branch into master"
git push origin master:master
```

# MySQL

### 解决A LEFT JOIN B 连接得到的新表C, 查询出来的记录总条数多于A表的记录总条数
#### 原因是A与B的关系不是1:1或1:0, 而是1:n(n > 1)导致A对应到B产生了多条数据. 此时要先处理B中重复的数据再与A做连接
```Mysql
SELECT A.xid, C.yid FROM xtable AS A LEFT JOIN (SELECT B.yid FROM ytable AS B GROUP BY B.yid) AS C ON A.xid = C.yid
```

# Windows
#### 查看PowerShell安装目录
```
$PsHome
```

#### 解决Terminal无法进入virtualenv的报错
1. 以管理员身份运行PowerShell
2. 执行get-ExecutionPolicy 回复Restricted, 表示状态是禁止的
3. 执行set-ExecutionPolicy RemoteSigned
4. 选择Y, 回车

#### windows使用Mac键位(https://www.zhihu.com/question/27564773)
```
下载AutoHotKey, 新建ahk文件, 填入以下内容

F11::suspend

$!c::
	SendInput {Ctrl Down}{c}{Ctrl Up}
Return
$!x::
	SendInput {Ctrl Down}{x}{Ctrl Up}
Return
$!v::
	SendInput {Ctrl Down}{v}{Ctrl Up}
Return
$!a::
	SendInput {Ctrl Down}{a}{Ctrl Up}
Return
$!s::
	SendInput {Ctrl Down}{s}{Ctrl Up}
Return
$!w::
	SendInput {Ctrl Down}{w}{Ctrl Up}
Return
$!z::
	SendInput {Ctrl Down}{z}{Ctrl Up}
Return
$!r::
	SendInput {Ctrl Down}{r}{Ctrl Up}
Return
$!t::
	SendInput {Ctrl Down}{t}{Ctrl Up}
Return
$!q::
	SendInput {Alt Down}{F4}{Alt Up}
Return
$!f::
	SendInput {Ctrl Down}{f}{Ctrl Up}
Return
$!/::
	SendInput {Ctrl Down}{/}{Ctrl Up}
Return
$^a::
	SendInput {Home}
Return
$^e::
	SendInput {End}
Return
$^u::
	SendInput {Shift Down}{Home}{Shift Up}{Backspace Down}{Backspace Up}
Return
$!LButton::
	SendInput {Ctrl Down}{Click Left}{Ctrl Up}
Return

```

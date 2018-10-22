# echo

### echo指令基本用法

```shell
 sudo echo --help

用法：echo [短选项]... [字符串]...
或：echo 长选项
 
将 STRING 回显到标准输出。
 
  -n 不尾随换行符
  -e 启用解释反斜杠的转义功能
  -E 禁用解释反斜杠的转义功能(默认)
      --help 显示此帮助信息并退出
      --version 显示版本信息并退出
若-e 可用，则以下序列即可识别：
  \\    反斜杠
  \a    响铃声
  \b    退格
  \c    不再产生新的输出
  \e    转义符  
  \f    换页
  \n    新行
  \r    回车
  \t    水平制表符
  \v    竖直制表符
  \0NNN   字节数以八进制数 NNN (1至3位)表示
  \xHH    字节数以十六进制数 HH (1至2位)表示
```

### 覆盖文件内容

test.sh
使用>指令覆盖文件原内容并重新输入内容，若文件不存在则创建文件。

```shell
#!/bin/bash
echo "Raspberry" > test.txt
    【操作过程】
# 修改权限，脚本可执行
chmod u+x test.sh    
./test.sh
    【文件内容】
Raspberry
```

### 追加文件内容

```shell
#!/bin/bash
echo "Raspberry" > test.txt
echo "Intel Galileo" >> test.txt
chmod u+x test.sh    
./test.sh
# 请注意echo指令默认在行尾增加回车(\n)，所以此处显示两行。
```

### 输入转移字符

```shell
#!/bin/bash
echo -e "{" > test-json.txt
echo -e "\t\"name\":\"xukai871105\"" >> test-json.txt
echo -e "}" >> test-json.txt
```

【说明】
    此处用到了两处转移字符，\t制表符，\"双引号。
    【操作过程】
修改权限，脚本可执行
chmod u+x test-json.sh    
./test-json.sh  
    【文件内容】
{
     "name":"xukai871105"
}

### 使用变量

上面的脚本中3处使用了文件名称test-json.txt，如果文件名称需要修改那么就需要修改3处，这样的操作显得麻烦些，为了简化操作可以使用变量简化脚本。
【示例脚本】test-json.sh

```shell
#!/bin/bash
FILE="test-json.txt"
echo -e "{" > $FILE
echo -e "\t\"name\":\"xukai871105\"" >> $FILE
echo -e "}" >> $FILE
```

【操作过程】
修改权限，脚本可执行
chmod u+x test-json.sh    
./test-json.sh  
    【文件内容】
{
     "name":"xukai871105"
}

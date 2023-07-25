### vim的三种模式

1. 插入模式：按i进入,在此模式下可以输入字符，按ESC将回到命令模式。
2. 命令模式：默认或esc进入,可以移动光标、删除字符等。
3. 低行模式：esc以后shift+: 可以保存文件、退出vi、设置vi、查找等功能(低行模式也可以看作是命令模式里的)。

vim的操作指南

以冒号开头的全是低行模式,其他基本上命令模式

进入vi的命令

```
vi filename :打开或新建文件，并将光标置于第一行首
vi +n filename ：打开文件，并将光标置于第n行首
vi + filename ：打开文件，并将光标置于最后一行首
vi +/pattern filename：打开文件，并将光标置于第一个与pattern匹配的串处
vi -r filename ：在上次正用vi编辑时发生系统崩溃，恢复filename
vi -o/O filename1 filename2 ... ：打开多个文件，依次进行编辑
vi 关闭文件
:w       //保存文件
:w vpser.net //保存至vpser.net文件
:q          //退出编辑器，如果文件已修改请使用下面的命令
:q!        //退出编辑器，且不保存
:wq         //退出编辑器，且保存文件 
```

移动光标类命令
```
l ：光标右移一个字符
space：光标右移一个字符
h ：光标左移一个字符
Backspace：光标左移一个字符
k或Ctrl+p：光标上移一行
j或Ctrl+n ：光标下移一行
Enter ：光标下移一行
w或W ：光标右移一个字至字首
e或E ：光标右移一个字至字尾
b或B ：光标左移一个字至字首
) ：光标移至句尾
( ：光标移至句首
}：光标移至段落开头
{：光标移至段落结尾
:100 跳到100行
:100+ 跳到101行
:100- 跳到99行
n$：光标移至第n行尾
nG: 光标移到第n行首
H ：光标移至屏幕顶行
M ：光标移至屏幕中间行
L ：光标移至屏幕最后行
0：（注意是数字零）光标移至当前行首
$：光标移至当前行尾
G: 跳至文件的底部
g: 文件开头
```

屏幕翻滚类命令
```
Ctrl+u：向文件首翻半屏
Ctrl+d：向文件尾翻半屏
Ctrl+f：向文件尾翻一屏
Ctrl+b；向文件首翻一屏
nz：将第n行滚至屏幕顶部，不指定n时将当前行滚至屏幕顶部。
插入文本类命令
i ：在光标前
I ：在当前行首
a：光标后
A：在当前行尾
o：在当前行之下新开一行
O：在当前行之上新开一行
r：替换当前字符
R：替换当前字符及其后的字符，直至按ESC键
s：删除当前光标处,并切换到插入模式
S：删除当前行,并切换到插入模式
```

复制、粘贴

```
yy    :将当前行复制到缓存区，也可以用 "ayy 复制，"a 为缓冲区，a也可以替换为a到z的任意字母，可以完成多个复制任务。
nyy   :将当前行向下n行复制到缓冲区，也可以用 "anyy 复制，"a 为缓冲区，a也可以替换为a到z的任意字母，可以完成多个复制任务。
yw    :复制从光标开始到词尾的字符。
nyw   :复制从光标开始的n个单词。
y^      :复制从光标到行首的内容。  
y$      :复制从光标到行尾的内容。
p        :粘贴剪切板里的内容在光标后，如果使用了前面的自定义缓冲区，建议使用"ap 进行粘贴。
P        :粘贴剪切板里的内容在光标前，如果使用了前面的自定义缓冲区，建议使用"aP 进行粘贴。
ayy 但是按a的时候就变成插入模式了... 怎么破?
```

搜索和替换命令

```
/pattern：从光标开始处向文件尾搜索pattern
?pattern：从光标开始处向文件首搜索pattern
n：在同一方向重复上一次搜索命令
N：在反方向上重复上一次搜索命令
s/p1/p2/g：将当前行中所有p1均用p2替代
:n1,n2s/p1/p2/g：将第n1至n2行中所有p1均用p2替代
:g/p1/s//p2/g：将文件中所有p1均用p2替换
:s/old/new      用new替换当前行中首次出现的old
:s/old/new/g    用new替换行中所有的old
:n,m s/old/new/g   用new替换从n到m行里所有的old
:%s/old/new/g      用new替换当前文件里所有的old
```

替换表达式

```
:%s/four/4/g
"%" 范围前缀表示在所有行中执行替换，最后的 "g" 标记表示替换行中的所有匹配点，如果仅仅对当前行进行操作，那么只要去掉%即可

如果你有一个像 "thirtyfour" 这样的单词，上面的命令会出错。这种情况下，这个单词会被替换成"thirty4″。要解决这个问题，用 "<"来指定匹配单词开头：

:%s/\<four/4/g 注意,要转译一下
显然，这样在处理 "fourty" 的时候还是会出错。用 ">" 来解决这个问题：

:%s/\<four\>/4/g
如果你在编码，你可能只想替换注释中的 "four"，而保留代码中的。由于这很难指定，可以在替换命令中加一个 "c" 标记，这样，Vim 会在每次替换前提示你：

:%s/\<four\>/4/gc
```

删除命令
```
ndw或ndW：删除光标处开始及其后的n-1个字
do：删至行首 报了一个错
d$：删至行尾
ndd：删除当前行及其后n-1行
x或X：删除一个字符，x删除光标后的，而X删除光标前的
Ctrl+u：删除输入方式下所输入的文本
x       删除当前字符
nx      删除从光标开始的n个字符
dd      删除当前行
ndd     向下删除当前行在内的n行
u       撤销上一步操作
U       撤销对当前行的所有操作
```

最后行方式命令

```
：n1,n2 co n3：将n1行到n2行之间的内容拷贝到第n3行下
：n1,n2 m n3：将n1行到n2行之间的内容移至到第n3行下
：n1,n2 d ：将n1行到n2行之间的内容删除
：w ：保存当前文件
：e filename：打开文件filename进行编辑
：x：保存当前文件并退出
：q：退出vi
：q!：不保存文件并退出vi
：!command：执行shell命令command
：n1,n2 w!command：将文件中n1行至n2行的内容作为command的输入并执行之，若不指定n1，n2，则表示将整个文件内容作为command的输入
：r!command：将命令command的输出结果放到当前行
:f 可以看文件名
```

多行注释和取消注释
多行注释：
```
进入命令行模式，按ctrl + v进入 visual block模式，然后按j, 或者k选中多行，把需要注释的行标记起来
按大写字母I，再插入注释符，例如//
按esc键就会全部注释了
取消多行注释：

进入命令行模式，按ctrl + v进入 visual block模式，按字母l横向选中列的个数，例如 // 需要选中2列
按字母j，或者k选中注释符号
按d键就可全部取消注释
```

vim的设置
```
在命令模式:
:set tabstop=2 设置tab制表符
:set nu 显示行号
:set nonu 不显示行号
:set autoindent 自动缩排
```
可以将配置添加到修改家目录下的.vimrc文件，这个文件是隐藏的文件,避免每次输入的麻烦,注意配置文件不要加上
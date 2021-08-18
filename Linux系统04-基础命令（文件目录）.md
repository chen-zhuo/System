# 基础命令（文件目录）

> **说明**：本文中对Linux命令的讲解都是基于名为CentOS的Linux发行版本，我自己使用的是阿里云服务器，系统版本为CentOS  8.4 64位。不同的Linux发行版本在Shell命令和工具程序上会有一些差别，但是这些差别是很小的。

**首先我们要知道一点，Linux系统当中没有输出错误就代表执行成功。**

**其次就是，所有Linux命令的参数都可以组合使用。**

**最后确保Linux命令是在英文模式下输入，而且尽量不要使用小键盘（数字键盘）。**

## 常用命令

### 查看|切换

查看目录内容 - **ls**

- `-a`：显示全部文件（包括以点开头的隐藏文件）和目录。
- `-l`：以长格式查看文件和目录。
- `-R`：遇到目录要进行递归展开（继续列出目录下面的文件和目录）。
- `-d`：只列出目录，不列出其他内容。
- `-S` / `-t`：按大小/时间排序。

![QQ截图20210805003133](Image/QQ截图20210805003133.png)

以树状图列出目录下的内容 - **tree**

- `-a` 显示所有文件和目录。
- `-C` 在文件和目录清单加上色彩，便于区分各种类型。
- `-d` 只显示目录名称而非内容。
- `-D` 列出文件或目录的更改时间。
- `-f` 在每个文件或目录之前，显示完整的相对路径名称。
- `-g` 列出文件或目录的所属群组名称，没有对应的名称时，则显示群组识别码。
- `-p` 列出权限标示。
- `-s` 列出文件或目录大小。
- `-t` 用文件和目录的更改时间排序。
- `-u` 列出文件或目录的拥有者名称，没有对应的名称时，则显示用户识别码。

![QQ截图20210812010012](Image/QQ截图20210812010012.png)

切换和查看当前工作目录 - **cd** / **pwd**。

- `cd`：快速切到家目录。
- `cd /`：快速到根目录。

绝对路径：以根目录开头的全部路径，即 `/` 开头的全部路径。

相对路径：以当前路径作为参照的全部路径。

> **`cd` 命令后面可以跟相对路径或绝对路径来切换到指定的目录， 且绝对路径在任何地方都可切换，而相对路径只能在当前路径下进行切换。**

返回上层：返回上一层路径，使用 `cd ..` 命令。

当前路径：查看当前位置绝对路径，使用 `pwd` 命令。

![QQ截图20210805005828](Image/QQ截图20210805005828.png)

> 在目录切换的过程中，命令前方显示的名称也在不断变化，它显示的是当前路径的目录名称。

### 创建|删除

创建目录 - **mkdir**

- `-p`：当目录不存在时，自动创建目录（递归创建）。

```
mkdir tmp：创建一个名称为tmp的新文件夹
mkdir tmp/Japan：创建一个名称为Japan的新文件夹（tmp文件夹必须存在）
```

![QQ截图20210810011254](Image/QQ截图20210810011254.png)

```
# 递归创建
mkdir -p tmp1/USA：创建一个名称为USA的新文件夹（tmp1文件夹可以不存在）
```

![QQ截图20210810012301](Image/QQ截图20210810012301.png)

```
# 多目录创建
mkdir tmp/Korea tmp1/China：同时创建名为USA和China的文件夹（tmp文件夹和tmp1文件夹必须存在必须存在）
```

![QQ截图20210810012744](Image/QQ截图20210810012744.png)

```
# 递归多目录创建
mkdir -p tmp2/Union tmp3/Russia：同时创建名为Union和Russia的文件夹（tmp2文件夹和tmp3文件夹可以不存在）
```

![QQ截图20210810013407](Image/QQ截图20210810013407.png)

删除**空**目录 -  **rmdir**

- `-p`：递归删除多个空目录。

```
rmdir /tmp/Japan：删除Japan目录（只能删除空目录）
```

![QQ截图20210812010707](Image/QQ截图20210812010707.png)

如果删除的目录里面还有一层目录，不管里面这层目录是否为空目录都删除不了，并且会提示：当前目录不为空。

![QQ截图20210812011013](Image/QQ截图20210812011013.png)

```
rmdir -p tmp/Korea/：删除tmp目录（递归删除多级空目录）
```

![QQ截图20210812011909](Image/QQ截图20210812011909.png)

删除文件或目录 - **rm**

##### 删除

- `-f`：就是 force 的意思，忽略不存在的文件，不会出现警告信息。
- `-i`：互动模式，在删除前会询问使用者是否动作。
- `-r`：递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！

!> `rm -rf /*` 递归强制删除根目录下的所有文件，跑路命令，切勿使用！虚拟机上可以玩玩。

![QQ截图20210813010924](Image/QQ截图20210813010924.png)

### 复制|移动|重命名

复制文件或目录 - **cp**

- 不加参数直接只能复制文件。

- `-r`：复制目录。

```
cp -r tmp1/China tmp2：将tmp1目录下的China目录复制到root目录下
```

![QQ截图20210813004519](Image/QQ截图20210813004519.png)

移动文件或目录 - **mv**

- `-b`：当目标文件或目录存在时，在执行覆盖前，会为其创建一个备份。
- `-i`：如果指定移动的源目录或文件与目标的目录或文件同名，则会先询问是否覆盖旧文件，输入 y 表示直接覆盖，输入 n 表示取消该操作。
- `-f`：如果指定移动的源目录或文件与目标的目录或文件同名，不会询问，直接覆盖旧文件。
- `-n`：不要覆盖任何已存在的文件或目录。
- `-u`：当源文件比目标文件新或者目标文件不存在时，才执行移动操作。

```
mv tmp3/Russia tmp2：将tmp3目录下的Russia目录移动到tmp2目录下
```

![QQ截图20210813005350](Image/QQ截图20210813005350.png)

重命名可以直接使用 `cp` 或 `mv` 命令来完成：

```
cp -r tmp1/USA tmp3/Japan：将USA目录复制到tmp3目录下并更名为Japan
mv tmp3 tmp：在同一文件夹下将tmp3文件夹更名为tmp
```

![QQ截图20210813010009](Image/QQ截图20210813010009.png)

## 基础属性

### 文件分类

**linux系统不同类型文件会有不同的颜色**，如下图：

![QQ截图20210814233404](Image/QQ截图20210814233404.png)

```
白色：表示普通文件
蓝色：表示目录
绿色：表示可执行文件
红色：表示压缩文件
浅蓝色：链接文件
红色闪烁：表示链接的文件有问题
黄色：表示设备文件
灰色：表示其他文件
```

### 文件属性

**前面讲过，Linux系统是一个稳定、安全的多用户系统。Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。**

我们可以使用 `ll` 或者 `ls –l` 命令来显示一个文件的属性以及文件所属的用户和组，如：

![QQ截图20210814172210](Image/QQ截图20210814172210.png)

每个文件的属性由左边第一部分的10个字符来确定（如下图）：

![vqwergbvbv](Image/vqwergbvbv.webp)

第一个字符代表目录、文件或链接文件等等：

- [ d ]代表目录；
- [ - ]代表文件；
- [ l ]代表链接文档 ( link file )，同时会显示指向的文件；
- [ b ]代表装置文件里面的可供储存的接口设备 ( 可随机存取装置 )；
- [ c ]代表装置文件里面的串行端口设备，例如键盘、鼠标 ( 一次性读取装置 )；

后面九个字符中，每三个字符为一组，且固定为『rwx』组合：

- [ r ]代表可读(read)；
- [ w ]代表可写(write)；
- [ x ]代表可执行(execute)；
- [ - ]代表没有该权限；
- 第1、4、7位表示读权限，用"r"字符表示，没有读权限，用"-"字符表示；
- 第2、5、8位表示写权限，用"w"字符表示，没有写权限，用"-"字符表示；
- 第3、6、9位表示执行权限，用"x"字符表示，没有执行权限，用"-"字符表示；

后面九个字符中，每三个字符为一组，代表不同的属主、属组、其他用户：

- 第1-3位确定属主（该文件的所有者）拥有该文件的权限；
- 第4-6位确定属组（所有者的同组用户）拥有该文件的权限；
- 第7-9位确定其他用户拥有该文件的权限；

**在Linux系统中，用户是按组分类的，一个用户属于一个或多个组。**

**每个文件都有一个特定的所有者，也就是对该文件具有所有权的用户，文件所有者以外的用户又可以分为"文件所有者的同组用户"和"其他用户"。**因此，Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限。

### 属性更改

更改文件属主 - **chown**

- `-R`：递归更改文件属主，更改某个目录文件的属主时，该目录下的所有文件的属主都会更改。

```
chown [–R] 属主名 文件名

# 只有管理员可以改变文件的所有者，所有者必须是存在的用户
chown root /tmp/a.file：将a文件的所有者改为root（不管是谁创建的）
```

更改文件属组 - **chgrp**

- `-R`：递归更改文件属组，更改某个目录文件的属组时，该目录下的所有文件的属组都会更改。

```
chgrp [-R] 属组名 文件名

# 只有管理员可以改变文件的所属组，所有者必须是存在的所属组
chgrp brother /tmp/a.file：将a文件的所属组更改为brother（不管是谁创建的）
```

更改文件权限 - **chmod**

- `-R`：递归更改文件权限，更改某个目录文件的权限时，该目录下的所有文件的权限都会更改。

```
chmod [-R] 数字/字符 文件或目录
```

目前最常用的就是通过数字更改文件的权限，权限数字对应关系：

```
读 —— r —— 4    写 —— w —— 2    执行 —— x —— 1  无权限 —— - —— 0

权限数字相加：
--- —— 0    --x —— 1    -w- —— 2    -wx —— 3
r-- —— 4    r-x —— 5    rw- —— 6    rwx —— 7

三个权限字符为一组：
--------- —— 000
r-x-wxrwx —— 567
...
rw-rw-rw- —— 666
rwxrwxrwx —— 777
```

![QQ截图20210815011653](Image/QQ截图20210815011653.png)

虽然改变了tmp1文件夹权限，但因为没有加上参数R，tmp1文件夹下的文件和文件夹的权限保持不变。

![QQ截图20210815012015](Image/QQ截图20210815012015.png)

另一种修改文件权限的方式就是通过字符进行修改：

```
chmod u+x Japan.list：给Japan.list文件的u（所有者）加x（执行权限）
chmod g+w Japan.list：给Japan.list文件的g（所属组）加w（写权限）
chmod o-r Japan.list：给Japan.list文件的o（其他人）减r（读权限）
chomd g=rwx Japan.list：给Japan.list文件的g（所属组）设置rwx（所有权限）
```

?> `umask -S`：显示创建文件夹的默认权限rwxr-xr-x

!> 注意：更改文件的权限只能是文件的所有者（文件创建者）或者是root（超级管理员）。

## 文件内容

### 内容查看

Linux中有许多查看文件内容的命令，根据使用场景选择合适的命令：

从第一行开始显示文件内容 - **cat**

- `-n`：列印出行号，连同空白行也会有行号。

![QQ截图20210819005639](Image/QQ截图20210819005639.png)

自带行号从第一行开始显示文件内容 - **nl**

![QQ截图20210819005837](Image/QQ截图20210819005837.png)

分页显示文件内容 - **more**

- 空格键或F键，向下翻页；Enter键下翻一行；q键退出

![QQ截图20210819010256](Image/QQ截图20210819010256.png)

分页显示文件内容 - **less**

- 上下键上下翻一行；PageUp键向上翻页；PageDown键向下翻页；q键退出

![QQ截图20210819011105](Image/QQ截图20210819011105.png)

查看文件内容开始几行 - **head**

- `-n`：后面接数字，代表显示几行的意思！

![QQ截图20210819011315](Image/QQ截图20210819011315.png)

查看文件内容结尾几行 - **tail**

- `-n`：后面接数字，代表显示几行的意思！

![QQ截图20210819011446](Image/QQ截图20210819011446.png)

### 内容查找

使用在 `less` 命令里面查找字符串 - **/字符串**或**?字符串**

- “/字符串”代表查找顺序从上到下；“?字符串”代表查找顺序从下到上
- n键，查找下一个字符串；N键，查找上一个字符串

![QQ截图20210819012322](Image/QQ截图20210819012322.png)

## 文本编辑器vim

 **Linux自带vi编辑器，vim是增强版的编辑器，但是需要安装才能使用。**

```
yum install vim
```

vim编辑器，有三种模式：

**命令模式（vim init.txt：打开init.txt，就进入命令模式）**
**编辑模式（命令模式下，按i键进入编辑模式，按ESC键，退出编辑模式，进入命令模式）**
**底行模式（命令模式下，输入:（英文冒号）进入底行模式）**

```
    命令模式：a : 在光标所在字符的后一个字符进入编辑模式
    		A : 在光标所在行末尾进入编辑模式
    		i : 在光标所在处进入编辑模式
    		I : 在当前行的第一个非空字符进入编辑模式
    		o : 在光标下新建一行进入编辑模式
    		O : 在光标所在行的上面新建一行进入编辑模式
    		s : 删除当前字符进入编辑模式
    		S : 删除当前行进入编辑模式
    		gg : 快速切换到第一行的行首
            G : 快速切换到最后一行的行首
            ngg : 快速切换到指定行的行首
            ^ : 快速切换到该行行首
            $ : 快速切换到该行行尾
            dd : 删除光标所在行
            u : 撤销操作
            ndd : 删除光标下n行，包含光标所在行
            yy : 复制光标所在行
            p : 粘贴复制的内容
            np : 复制几次
            nyy : 复制光标下n行，包含光标所在行
            4dd : 删除和前切光标下面的4行
		# 翻页
            ctrl + f : 下一页  forward(pagedown键)
            ctrl + b : 上一页  backward(pageup键)
            ctrl + d : 下翻半页 down
            ctrl + u : 上翻半页 up
    底行模式：
    	# 保存
        	输入 :w：保存修改
        	输入 :w /tmp/new_file：另存为tmp下的指定文件
        	输入 :wq：保存并且退出
        	输入 :wq!：强制保存并且退出（文件所有者和root能使用）
        	输入 :q!：不保存，强制退出
    	# 行号
    		输入 :set nu：就会显示行号
        	输入 :set nonu：取消显示行号
        # 跳跃
        	输入 :1000：快速跳到1000行
        # 删除
        	输入 :1000，1002d：删除1000行到1002行
        # 查找
        	输入 :/ftp：查找含有ftp的内容（按n查找下一个）
        # 替换
          光标所在行
            输入 :s/孤单/幸福   将光标所在行的第一个孤单替换为幸福
            输入 :s/孤单/幸福/g   将光标所在行的所有孤单替换为幸福
          指定行
            输入 :n,ms/孤单/幸福  将n到m行第一个孤单替换为幸福
            输入 :n,ms/孤单/幸福/g  将n到m行所有孤单替换为幸福
          所有行
            输入 :%s/ftp/ym	将全文的第一个ftp替换为ym
            输入 :%s/ftp/ym/g	将全文的ftp替换为ym
```

常见错误：非法编辑退出vi的时候，会产生一个 .文件名.后缀名.swp 的交换文件，只要有这个文件存在, 那么打开这个文件的时候就会有提示，不想要这个提示，删除这个文件即可。

```
rm -f .2.txt.swpvi -r 2.txt   恢复到上次编辑的内容
```

### 编辑器 - vim

1. 启动vim。可以通过`vi`或`vim`命令来启动vim，启动时可以指定文件名来打开一个文件，如果没有指定文件名，也可以在保存的时候指定文件名。

    ```
    [root ~]# vim guess.py
    ```

2. 命令模式、编辑模式和末行模式：启动vim进入的是命令模式（也称为Normal模式），在命令模式下输入英文字母`i`会进入编辑模式（Insert模式），屏幕下方出现`-- INSERT --`提示；在编辑模式下按下`Esc`会回到命令模式，此时如果输入英文`:`会进入末行模式，在末行模式下输入`q!`可以在不保存当前工作的情况下强行退出vim；在命令模式下输入`v`会进入可视模式（Visual模式），可以用光标选择一个区域再完成对应的操作。

3. 保存和退出vim：在命令模式下输入`:` 进入末行模式，输入`wq`可以实现保存退出；如果想放弃编辑的内容输入`q!`强行退出，这一点刚才已经提到过了；在命令模式下也可以直接输入`ZZ`实现保存退出。如果只想保存文件不退出，那么可以在末行模式下输入`w`；可以在`w`后面输入空格再指定要保存的文件名。

4. 光标操作。

    - 在命令模式下可以通过`h`、`j`、`k`、`l`来控制光标向左、下、上、右的方向移动，可以在字母前输入数字来表示移动的距离，例如：`10h`表示向左移动10个字符。
    - 在命令模式下可以通过`Ctrl+y`和`Ctrl+e`来实现向上、向下滚动一行文本的操作，可以通过`Ctrl+f`和`Ctrl+b`来实现向前和向后翻页的操作。
    - 在命令模式下可以通过输入英文字母`G`将光标移到文件的末尾，可以通过`gg`将光标移到文件的开始，也可以通过在`G`前输入数字来将光标移动到指定的行。

5. 文本操作。

    - 删除：在命令模式下可以用`dd`来删除整行；可以在`dd`前加数字来指定删除的行数；可以用`d$`来实现删除从光标处删到行尾的操作，也可以通过`d0`来实现从光标处删到行首的操作；如果想删除一个单词，可以使用`dw`；如果要删除全文，可以在输入`:%d`（其中`:`用来从命令模式进入末行模式）。
    - 复制和粘贴：在命令模式下可以用`yy`来复制整行；可以在`yy`前加数字来指定复制的行数；可以通过`p`将复制的内容粘贴到光标所在的地方。
    - 撤销和恢复：在命令模式下输入`u`可以撤销之前的操作；通过`Ctrl+r`可以恢复被撤销的操作。
    - 对内容进行排序：在命令模式下输入`%!sort`。

6. 查找和替换。

    - 查找操作需要输入`/`进入末行模式并提供正则表达式来匹配与之对应的内容，例如：`/doc.*\.`，输入`n`来向前搜索，也可以输入`N`来向后搜索。

    - 替换操作需要输入

        ```
        :
        ```

        进入末行模式并指定搜索的范围、正则表达式以及替换后的内容和匹配选项，例如：

        ```
        :1,$s/doc.*/hello/gice
        ```

        ，其中：

        - `g` - global：全局匹配。
        - `i` - ignore case：忽略大小写匹配。
        - `c` - confirm：替换时需要确认。
        - `e` - error：忽略错误。

7. 参数设定：在输入`:`进入末行模式后可以对vim进行设定。

    - 设置Tab键的空格数：`set ts=4`

    - 设置显示/不显示行号：`set nu` / `set nonu`

    - 设置启用/关闭高亮语法：`syntax on` / `syntax off`

    - 设置显示标尺（光标所在的行和列）： `set ruler`

    - 设置启用/关闭搜索结果高亮：`set hls` / `set nohls`

        > 说明：如果希望上面的这些设定在每次启动vim时都能自动生效，需要将这些设定写到用户主目录下的.vimrc文件中。

8. 高级技巧

    - 比较多个文件。

        ```
        [root ~]# vim -d foo.txt bar.txt
        ```

        [![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day31-35/res/vim-diff.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day31-35/res/vim-diff.png)

    - 打开多个文件。

        ```
        [root ~]# vim foo.txt bar.txt hello.txt
        ```

        启动vim后只有一个窗口显示的是foo.txt，可以在末行模式中输入`ls`查看到打开的三个文件，也可以在末行模式中输入`b <num>`来显示另一个文件，例如可以用`:b 2`将bar.txt显示出来，可以用`:b 3`将hello.txt显示出来。

    - 拆分和切换窗口。

        可以在末行模式中输入`sp`或`vs`来实现对窗口的水平或垂直拆分，这样我们就可以同时打开多个编辑窗口，通过按两次`Ctrl+w`就可以实现编辑窗口的切换，在一个窗口中执行退出操作只会关闭对应的窗口，其他的窗口继续保留。

        [![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day31-35/res/vim-multi-window.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day31-35/res/vim-multi-window.png)

    - 映射快捷键：在vim下可以将一些常用操作映射为快捷键来提升工作效率。

        - 例子1：在命令模式下输入`F4`执行从第一行开始删除10000行代码的操作。

            `:map <F4> gg10000dd`。

            例子2：在编辑模式下输入`__main`直接补全为`if __name__ == '__main__':`。

            `:inoremap __main if __name__ == '__main__':`

        > 说明：上面例子2的`inoremap`中的`i`表示映射的键在编辑模式使用， `nore`表示不要递归，这一点非常重要，否则如果键对应的内容中又出现键本身，就会引发递归（相当于进入了死循环）。如果希望映射的快捷键每次启动vim时都能生效，需要将映射写到用户主目录下的.vimrc文件中。

    - 录制宏。

        - 在命令模式下输入`qa`开始录制宏（其中`a`是寄存器的名字，也可以是其他英文字母或0-9的数字）。

        - 执行你的操作（光标操作、编辑操作等），这些操作都会被录制下来。

        - 如果录制的操作已经完成了，按`q`结束录制。

        - 通过`@a`（`a`是刚才使用的寄存器的名字）播放宏，如果要多次执行宏可以在前面加数字，例如`100@a`表示将宏播放100次。

        - 可以试一试下面的例子来体验录制宏的操作，该例子来源于[Harttle Land网站](https://harttle.land/tags.html#Vim)，该网站上提供了很多关于vim的使用技巧，有兴趣的可以了解一下。

            [![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day31-35/res/vim-macro.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day31-35/res/vim-macro.png)

##### 复制、粘贴

```
vim init.log：打开文件init.log:r /etc/issue：将issue文件的内容，导入init.log文件中:r !date：将当前时间导入init.log文件中
```











## 运行

### 关机重启

在linux领域内大多用在服务器上，很少遇到关机的操作。毕竟服务器上跑一个服务是永无止境的，除非特殊情况下，不得已才会关机。**但不管是重启系统还是关闭系统，首先要运行 `sync` 命令，把内存中的数据写到磁盘中。**

```
sync # 将数据由内存同步到硬盘中。

shutdown # 关机指令，你可以man shutdown 来看一下帮助文档。例如你可以运行如下命令关机：

shutdown –h 10 # 这个命令告诉大家，计算机将在10分钟后关机

shutdown –h now # 立马关机

shutdown –h 20:25 # 系统会在今天20:25关机

shutdown –h +10 # 十分钟后关机

shutdown –r now # 系统立马重启

shutdown –r +10 # 系统十分钟后重启

reboot # 立即重启，等同于 shutdown –r now

halt # 关闭系统，等同于shutdown –h now 和 poweroff
```

重启和关机 - **reboot** / **shutdown**。

> 说明：在执行`shutdown`命令时会向登录系统的用户发出警告，可以在命令后面跟上警告消息来替换默认的警告消息，也可以在`-h`参数后通过`now`来表示立刻关机。















##### sudo权限

```
# 给普通用户赋予超级用户才能执行的命令权限，前提是要root修改sudo命令的配置文件，给出权利才能使用sudo
sudo -l：查看能使用超级管理员才能执行的命令
sudo 命令的绝对路径 命令：执行超级管理员才能执行的命令
sudo /sbin/shtdown -r now：执行这条命令的前提是超级管理员给了这条命令的权限
```

##### ACL权限

ACL权限用于身份不足的情况（即所有者、所属组、其他人，三种情况外）。相当于不给用户添加身份，直接给他权限。

```
df -h：查询系统分区状况

dumpe2fs -h/dev/sda5：查询指定分区详细文件系统信息（sda5就是上面命令查询显示的root分区）（在当中查看Default mount options这行是否有acl，有就表明能开启ACL权限）

mount -o remount,acl/：重新挂载根分区，并加入acl权限（临时挂载）

vim /etc/fstab：修改配置文件（UUID=c2....../ ext4 defaults,acl 1 1）（加入acl,永久挂载）
mount -o remount/：挂在后重启生效
```

##### chattr权限

```
chattr +i 文件或目录：改变文件或目录权限
（+：增加权限，-：删除权限，=：等于某权限）
（i：锁住文件，不能对文件删除、改名，也不能修改文件数据；如果是目录，只能修改目录下文件的数据，但不能建立和删除文件，root也会受到该限制。a：如果是文件，只能在文件中增加数据，但不能删除也不能修改数据；如果是目录，只能在目录中建立和修改文件，但不能删除）

lsattr -a abc：查看abc文件属性（-a显示所有文件和目录，-d若目标是目录，列出目录本身的属性）
```



Linux系统的命令通常都是如下所示的格式：

```
命令名称 [命名参数] [命令对象]
```

1. 获取登录信息 - **w** / **who** / **last**/ **lastb**。

    ```
    [root ~]# w
     23:31:16 up 12:16,  2 users,  load average: 0.00, 0.01, 0.05
    USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
    root     pts/0    182.139.66.250   23:03    4.00s  0.02s  0.00s w
    jackfrue pts/1    182.139.66.250   23:26    3:56   0.00s  0.00s -bash
    [root ~]# who
    root     pts/0        2018-04-12 23:03 (182.139.66.250)
    jackfrued pts/1        2018-04-12 23:26 (182.139.66.250)
    [root ~]# who am i
    root     pts/0        2018-04-12 23:03 (182.139.66.250)
    [root ~]# who mom likes
    root     pts/0        2018-04-12 23:03 (182.139.66.250)
    [root ~]# last
    root     pts/0        117.136.63.184   Sun May 26 18:57   still logged in   
    reboot   system boot  3.10.0-957.10.1. Mon May 27 02:52 - 19:10  (-7:-42)   
    root     pts/4        117.136.63.184   Sun May 26 18:51 - crash  (08:01)    
    root     pts/4        117.136.63.184   Sun May 26 18:49 - 18:49  (00:00)    
    root     pts/3        117.136.63.183   Sun May 26 18:35 - crash  (08:17)    
    root     pts/2        117.136.63.183   Sun May 26 18:34 - crash  (08:17)    
    root     pts/0        117.136.63.183   Sun May 26 18:10 - crash  (08:42)    
    ```

2. 查看自己使用的Shell - **ps**。

    Shell也被称为“壳”或“壳程序”，它是用户与操作系统内核交流的翻译官，简单的说就是人与计算机交互的界面和接口。目前很多Linux系统默认的Shell都是bash（Bourne Again SHell），因为它可以使用tab键进行命令和路径补全、可以保存历史命令、可以方便的配置环境变量以及执行批处理操作。

    ```
    [root ~]# ps
      PID TTY          TIME CMD
     3531 pts/0    00:00:00 bash
     3553 pts/0    00:00:00 ps
    ```

3. 查看命令的说明和位置 - **whatis** / **which** / **whereis**。

    ```
    [root ~]# whatis ps
    ps (1)        - report a snapshot of the current processes.
    [root ~]# whatis python
    python (1)    - an interpreted, interactive, object-oriented programming language
    [root ~]# whereis ps
    ps: /usr/bin/ps /usr/share/man/man1/ps.1.gz
    [root ~]# whereis python
    python: /usr/bin/python /usr/bin/python2.7 /usr/lib/python2.7 /usr/lib64/python2.7 /etc/python /usr/include/python2.7 /usr/share/man/man1/python.1.gz
    [root ~]# which ps
    /usr/bin/ps
    [root ~]# which python
    /usr/bin/python
    ```

4. 清除屏幕上显示的内容 - **clear**。

5. 查看帮助文档 - **man** / **info** / **--help** / **apropos**。

    ```
    [root@izwz97tbgo9lkabnat2lo8z ~]# ps --help
    Usage:
     ps [options]
     Try 'ps --help <simple|list|output|threads|misc|all>'
      or 'ps --help <s|l|o|t|m|a>'
     for additional help text.
    For more details see ps(1).
    [root@izwz97tbgo9lkabnat2lo8z ~]# man ps
    PS(1)                                User Commands                                PS(1)
    NAME
           ps - report a snapshot of the current processes.
    SYNOPSIS
           ps [options]
    DESCRIPTION
    ...
    ```

6. 查看系统和主机名 - **uname** / **hostname**。

    ```
    [root@izwz97tbgo9lkabnat2lo8z ~]# uname
    Linux
    [root@izwz97tbgo9lkabnat2lo8z ~]# hostname
    izwz97tbgo9lkabnat2lo8z
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
    CentOS Linux release 7.6.1810 (Core)
    ```

    > 说明：`cat`是连接文件内容并打印到标准输出的命令，后面会讲到该命令；`/etc`是Linux系统上的一个非常重要的目录，它保存了很多的配置文件；`centos-release`是该目录下的一个文件，因为我自己使用的Linux发行版本是CentOS 7.6，因此这里会有一个这样的文件。

7. 时间和日期 - **date** / **cal**。

    ```
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# date
    Wed Jun 20 12:53:19 CST 2018
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal
          June 2018
    Su Mo Tu We Th Fr Sa
                    1  2
     3  4  5  6  7  8  9
    10 11 12 13 14 15 16
    17 18 19 20 21 22 23
    24 25 26 27 28 29 30
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal 5 2017
          May 2017
    Su Mo Tu We Th Fr Sa
        1  2  3  4  5  6
     7  8  9 10 11 12 13
    14 15 16 17 18 19 20
    21 22 23 24 25 26 27
    28 29 30 31
    ```

    

9. 退出登录 - **exit** / **logout**。

10. 查看历史命令 - **history**。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# history
...
452  ls
453  cd Python-3.6.5/
454  clear
455  history
[root@iZwz97tbgo9lkabnat2lo8Z ~]# !454
```

> **说明**：查看到历史命令之后，可以用`!历史命令编号`来重新执行该命令；通过`history -c`可以清除历史命令。

2. 创建/删除文件 - **touch** / **rm**。

    ```
    [root ~]# touch readme.txt[root ~]# touch error.txt[root ~]# rm error.txtrm: remove regular empty file ‘error.txt’? y[root ~]# rm -rf xyz
    ```

    - ```
        touch
        ```

        命令用于创建空白文件或修改文件时间。在Linux系统中一个文件有三种时间：

        - 更改内容的时间 - mtime。
        - 更改权限的时间 - ctime。
        - 最后访问时间 - atime。

    - ```
        rm
        ```

        的几个重要参数：

        - `-i`：交互式删除，每个删除项都会进行询问。
        - `-r`：删除目录并递归的删除目录中的文件和目录。
        - `-f`：强制删除，忽略不存在的文件，没有任何提示。

5. 查看文件内容 - **cat** / **tac** / **head** / **tail** / **more** / **less** / **rev** / **od**。

    ```
    [root ~]# wget http://www.sohu.com/ -O sohu.html--2018-06-20 18:42:34--  http://www.sohu.com/Resolving www.sohu.com (www.sohu.com)... 14.18.240.6Connecting to www.sohu.com (www.sohu.com)|14.18.240.6|:80... connected.HTTP request sent, awaiting response... 200 OKLength: 212527 (208K) [text/html]Saving to: ‘sohu.html’100%[==================================================>] 212,527     --.-K/s   in 0.03s2018-06-20 18:42:34 (7.48 MB/s) - ‘sohu.html’ saved [212527/212527][root ~]# cat sohu.html...[root ~]# head -10 sohu.html<!DOCTYPE html><html><head><title>搜狐</title><meta name="Keywords" content="搜狐,门户网站,新媒体,网络媒体,新闻,财经,体育,娱乐,时尚,汽车,房产,科技,图片,论坛,微博,博客,视频,电影,电视剧"/><meta name="Description" content="搜狐网为用户提供24小时不间断的最新资讯，及搜索、邮件等网络服务。内容包括全球热点事件、突发新闻、时事评论、热播影视剧、体育赛事、行业动态、生活服务信息，以及论坛、博客、微博、我的搜狐等互动空间。" /><meta name="shenma-site-verification" content="1237e4d02a3d8d73e96cbd97b699e9c3_1504254750"><meta charset="utf-8"/><meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"/>[root ~]# tail -2 sohu.html</body></html>[root ~]# less sohu.html...[root ~]# cat -n sohu.html | more...
    ```

    > **说明**：上面用到了一个名为`wget`的命令，它是一个网络下载器程序，可以从指定的URL下载资源。

6. 拷贝/移动文件 - **cp** / **mv**。

    ```
    [root ~]# mkdir backup[root ~]# cp sohu.html backup/[root ~]# cd backup[root backup]# lssohu.html[root backup]# mv sohu.html sohu_index.html[root backup]# lssohu_index.html
    ```

7. 文件重命名 - **rename**。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# rename .htm .html *.htm
```

1. 查找文件和查找内容 - **find** / **grep**。

    ```
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# find / -name "*.html"
    /root/sohu.html
    /root/backup/sohu_index.html
    [root@izwz97tbgo9lkabnat2lo8z ~]# find . -atime 7 -type f -print
    [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -size +2k
    [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -name "*.swp" -delete
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# grep "<script>" sohu.html -n
    20:<script>
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# grep -E \<\/?script.*\> sohu.html -n
    20:<script>
    22:</script>
    24:<script src="//statics.itc.cn/web/v3/static/js/es5-shim-08e41cfc3e.min.js"></script>
    25:<script src="//statics.itc.cn/web/v3/static/js/es5-sham-1d5fa1124b.min.js"></script>
    26:<script src="//statics.itc.cn/web/v3/static/js/html5shiv-21fc8c2ba6.js"></script>
    29:<script type="text/javascript">
    52:</script>
    ...
    ```

    > **说明**：`grep`在搜索字符串时可以使用正则表达式，如果需要使用正则表达式可以用`grep -E`或者直接使用`egrep`。

2. 创建链接和查看链接 - **ln** / **readlink**。

    ```
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
    -rw-r--r-- 1 root root 212131 Jun 20 19:15 sohu.html
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
    -rw-r--r-- 2 root root 212131 Jun 20 19:15 sohu.html
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup2
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
    -rw-r--r-- 3 root root 212131 Jun 20 19:15 sohu.html
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln -s /etc/centos-release sysinfo
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sysinfo
    lrwxrwxrwx 1 root root 19 Jun 20 19:21 sysinfo -> /etc/centos-release
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat sysinfo
    CentOS Linux release 7.4.1708 (Core)
    [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
    CentOS Linux release 7.4.1708 (Core)
    ```

    > **说明**：链接可以分为硬链接和软链接（符号链接）。硬链接可以认为是一个指向文件数据的指针，就像Python中对象的引用计数，每添加一个硬链接，文件的对应链接数就增加1，只有当文件的链接数为0时，文件所对应的存储空间才有可能被其他文件覆盖。我们平常删除文件时其实并没有删除硬盘上的数据，我们删除的只是一个指针，或者说是数据的一条使用记录，所以类似于“文件粉碎机”之类的软件在“粉碎”文件时除了删除文件指针，还会在文件对应的存储区域填入数据来保证文件无法再恢复。软链接类似于Windows系统下的快捷方式，当软链接链接的文件被删除时，软链接也就失效了。

3. 压缩/解压缩和归档/解归档 - **gzip** / **gunzip** / **xz**。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://download.redis.io/releases/redis-4.0.10.tar.gz--2018-06-20 19:29:59--  http://download.redis.io/releases/redis-4.0.10.tar.gzResolving download.redis.io (download.redis.io)... 109.74.203.151Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.HTTP request sent, awaiting response... 200 OKLength: 1738465 (1.7M) [application/x-gzip]Saving to: ‘redis-4.0.10.tar.gz’100%[==================================================>] 1,738,465   70.1KB/s   in 74s2018-06-20 19:31:14 (22.9 KB/s) - ‘redis-4.0.10.tar.gz’ saved [1738465/1738465][root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*redis-4.0.10.tar.gz[root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip redis-4.0.10.tar.gz[root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*redis-4.0.10.tar
```

1. 归档和解归档 - **tar**。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf redis-4.0.10.tarredis-4.0.10/redis-4.0.10/.gitignoreredis-4.0.10/00-RELEASENOTESredis-4.0.10/BUGSredis-4.0.10/CONTRIBUTINGredis-4.0.10/COPYINGredis-4.0.10/INSTALLredis-4.0.10/MANIFESTOredis-4.0.10/Makefileredis-4.0.10/README.mdredis-4.0.10/deps/redis-4.0.10/deps/Makefileredis-4.0.10/deps/README.md...
```

> 说明：归档（也称为创建归档）和解归档都使用`tar`命令，通常创建归档需要`-cvf`三个参数，其中`c`表示创建（create），`v`表示显示创建归档详情（verbose），`f`表示指定归档的文件（file）；解归档需要加上`-xvf`参数，其中`x`表示抽取（extract），其他两个参数跟创建归档相同。

1. 将标准输入转成命令行参数 - **xargs**。

下面的命令会将查找当前路径下的html文件，然后通过`xargs`将这些文件作为参数传给`rm`命令，实现查找并删除文件的操作。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# find . -type f -name "*.html" | xargs rm -f
```

下面的命令将a.txt文件中的多行内容变成一行输出到b.txt文件中，其中`<`表示从a.txt中读取输入，`>`表示将命令的执行结果输出到b.txt中。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# xargs < a.txt > b.txt
```

> **说明**：这个命令就像上面演示的那样常在管道（实现进程间通信的一种方式）和重定向（重新指定输入输出的位置）操作中用到，后面的内容中会讲到管道操作和输入输出重定向操作。

1. 显示文件或目录 - **basename** / **dirname**。
2. 其他相关工具。

- **sort** - 对内容排序
- **uniq** - 去掉相邻重复内容
- **tr** - 替换指定内容为新内容
- **cut** / **paste** - 剪切/黏贴内容
- **split** - 拆分文件
- **file** - 判断文件类型
- **wc** - 统计文件行数、单词数、字节数
- **iconv** - 编码转换

```
[root ~]# cat foo.txtgrapeapplepitaya[root ~]# cat bar.txt100200300400[root ~]# paste foo.txt bar.txtgrape   100apple   200pitaya  300        400[root ~]# paste foo.txt bar.txt > hello.txt[root ~]# cut -b 4-8 hello.txtpe      10le      20aya     30[root ~]# cat hello.txt | tr '\t' ','grape,100apple,200pitaya,300,400[root ~]# split -l 100 sohu.html hello[root ~]# wget https://www.baidu.com/img/bd_logo1.png[root ~]# file bd_logo1.pngbd_logo1.png: PNG image data, 540 x 258, 8-bit colormap, non-interlaced[root ~]# wc sohu.html  2979   6355 212527 sohu.html[root ~]# wc -l sohu.html2979 sohu.html[root ~]# wget http://www.qq.com -O qq.html[root ~]# iconv -f gb2312 -t utf-8 qq.html
```

#### 管道和重定向

1. 管道的使用 - **|**。

    例子：查找当前目录下文件个数。

    ```
    [root ~]# find ./ | wc -l6152
    ```

    例子：列出当前路径下的文件和文件夹，给每一项加一个编号。

    ```
    [root ~]# ls | cat -n     1  dump.rdb     2  mongodb-3.6.5     3  Python-3.6.5     4  redis-3.2.11     5  redis.conf
    ```

    例子：查找record.log中包含AAA，但不包含BBB的记录的总数

    ```
    [root ~]# cat record.log | grep AAA | grep -v BBB | wc -l
    ```

2. 输出重定向和错误重定向 - **>** / **>>** / **2>**。

    ```
    [root ~]# cat readme.txtbananaapplegrapeapplegrapewatermelonpearpitaya[root ~]# cat readme.txt | sort | uniq > result.txt[root ~]# cat result.txtapplebananagrapepearpitayawatermelon
    ```

3. 输入重定向 - **<**。

    ```
    [root ~]# echo 'hello, world!' > hello.txt[root ~]# wall < hello.txt[root ~]#Broadcast message from root (Wed Jun 20 19:43:05 2018):hello, world![root ~]# echo 'I will show you some code.' >> hello.txt[root ~]# wall < hello.txt[root ~]#Broadcast message from root (Wed Jun 20 19:43:55 2018):hello, world!I will show you some code.
    ```

4. 多重定向 - **tee**。

    下面的命令除了在终端显示命令`ls`的结果之外，还会追加输出到`ls.txt`文件中。

    ```
    [root ~]# ls | tee -a ls.txt
    ```

#### 别名

1. **alias**

    ```
    [root ~]# alias ll='ls -l'[root ~]# alias frm='rm -rf'[root ~]# ll...drwxr-xr-x  2 root       root   4096 Jun 20 12:52 abc...[root ~]# frm abc
    ```

2. **unalias**

    ```
    [root ~]# unalias frm[root ~]# frm sohu.html-bash: frm: command not found
    ```

#### 文本处理

1. 字符流编辑器 - **sed**。

    sed是操作、过滤和转换文本内容的工具。假设有一个名为fruit.txt的文件，内容如下所示。

    ```
    [root ~]# cat -n fruit.txt 
         1  banana
         2  grape
         3  apple
         4  watermelon
         5  orange
    ```

    接下来，我们在第2行后面添加一个pitaya。

    ```
    [root ~]# sed '2a pitaya' fruit.txt 
    banana
    grape
    pitaya
    apple
    watermelon
    orange
    ```

    > 注意：刚才的命令和之前我们讲过的很多命令一样并没有改变fruit.txt文件，而是将添加了新行的内容输出到终端中，如果想保存到fruit.txt中，可以使用输出重定向操作。

    在第2行前面插入一个waxberry。

    ```
    [root ~]# sed '2i waxberry' fruit.txt
    banana
    waxberry
    grape
    apple
    watermelon
    orange
    ```

    删除第3行。

    ```
    [root ~]# sed '3d' fruit.txt
    banana
    grape
    watermelon
    orange
    ```

    删除第2行到第4行。

    ```
    [root ~]# sed '2,4d' fruit.txt
    banana
    orange
    ```

    将文本中的字符a替换为@。

    ```
    [root ~]# sed 's#a#@#' fruit.txt 
    b@nana
    gr@pe
    @pple
    w@termelon
    or@nge
    ```

    将文本中的字符a替换为@，使用全局模式。

    ```
    [root ~]# sed 's#a#@#g' fruit.txt b@n@n@gr@pe@pplew@termelonor@nge
    ```

2. 模式匹配和处理语言 - **awk**。

    awk是一种编程语言，也是Linux系统中处理文本最为强大的工具，它的作者之一和现在的维护者就是之前提到过的Brian Kernighan（ken和dmr最亲密的伙伴）。通过该命令可以从文本中提取出指定的列、用正则表达式从文本中取出我们想要的内容、显示指定的行以及进行统计和运算，总之它非常强大。

    假设有一个名为fruit2.txt的文件，内容如下所示。

    ```
    [root ~]# cat fruit2.txt 1       banana      1202       grape       5003       apple       12304       watermelon  805       orange      400
    ```

    显示文件的第3行。

    ```
    [root ~]# awk 'NR==3' fruit2.txt 3       apple       1230
    ```

    显示文件的第2列。

    ```
    [root ~]# awk '{print $2}' fruit2.txt 
    banana
    grape
    apple
    watermelon
    orange
    ```

    显示文件的最后一列。

    ```
    [root ~]# awk '{print $NF}' fruit2.txt 
    120
    500
    1230
    80
    400
    ```

    输出末尾数字大于等于300的行。

    ```
    [root ~]# awk '{if($3 >= 300) {print $0}}' fruit2.txt 
    2       grape       500
    3       apple       1230
    5       orange      400
    ```

    上面展示的只是awk命令的冰山一角，更多的内容留给读者自己在实践中去探索。

### 用户管理

1. 创建和删除用户 - **useradd** / **userdel**。

    ```
    [root home]# useradd hellokitty
    [root home]# userdel hellokitty
    ```

    - `-d` - 创建用户时为用户指定用户主目录
    - `-g` - 创建用户时指定用户所属的用户组

2. 创建和删除用户组 - **groupadd** / **groupdel**。

    > 说明：用户组主要是为了方便对一个组里面所有用户的管理。

3. 修改密码 - **passwd**。

    ```
    [root ~]# passwd hellokitty
    New password: 
    Retype new password: 
    passwd: all authentication tokens updated successfully.
    ```

    > 说明：输入密码和确认密码没有回显且必须一气呵成的输入完成（不能使用退格键），密码和确认密码需要一致。如果使用`passwd`命令时没有指定命令作用的对象，则表示要修改当前用户的密码。如果想批量修改用户密码，可以使用`chpasswd`命令。

    - `-l` / `-u` - 锁定/解锁用户。
    - `-d` - 清除用户密码。
    - `-e` - 设置密码立即过期，用户登录时会强制要求修改密码。
    - `-i` - 设置密码过期多少天以后禁用该用户。

4. 查看和修改密码有效期 - **chage**。

    设置hellokitty用户100天后必须修改密码，过期前15天通知该用户，过期后15天禁用该用户。

    ```
    chage -M 100 -W 15 -I 7 hellokitty
    ```

5. 切换用户 - **su**。

    ```
    [root ~]# su hellokitty[hellokitty root]$
    ```

6. 以管理员身份执行命令 - **sudo**。

    ```
    [hellokitty ~]$ ls /rootls: cannot open directory /root: Permission denied[hellokitty ~]$ sudo ls /root[sudo] password for hellokitty:
    ```

    > **说明**：如果希望用户能够以管理员身份执行命令，用户必须要出现在sudoers名单中，sudoers文件在 `/etc`目录下，如果希望直接编辑该文件也可以使用下面的命令。

7. 编辑sudoers文件 - **visudo**。

    这里使用的编辑器是vi，关于vi的知识在后面有讲解。该文件的部分内容如下所示：

    ```
    ## Allow root to run any commands anywhere root    ALL=(ALL)   ALL## Allows members of the 'sys' group to run networking, software, ## service management apps and more.# %sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES, LOCATE, DRIVERS## Allows people in group wheel to run all commands%wheel  ALL=(ALL)   ALL## Same thing without a password# %wheel    ALL=(ALL)   NOPASSWD: ALL## Allows members of the users group to mount and unmount the## cdrom as root# %users  ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom## Allows members of the users group to shutdown this system# %users  localhost=/sbin/shutdown -h now
    ```

8. 显示用户与用户组的信息 - **id**。

9. 给其他用户发消息 -**write** / **wall**。

    发送方：

    ```
    [root ~]# write hellokittyDinner is on me.Call me at 6pm.
    ```

    接收方：

    ```
    [hellokitty ~]$ Message from root on pts/0 at 17:41 ...Dinner is on me.Call me at 6pm.EOF
    ```

10. 查看/设置是否接收其他用户发送的消息 - **mesg**。

```
[hellokitty ~]$ mesgis y[hellokitty ~]$ mesg n[hellokitty ~]$ mesgis n
```

### 文件系统

#### 文件和路径

1. 命名规则：文件名的最大长度与文件系统类型有关，一般情况下，文件名不应该超过255个字符，虽然绝大多数的字符都可以用于文件名，但是最好使用英文大小写字母、数字、下划线、点这样的符号。文件名中虽然可以使用空格，但应该尽可能避免使用空格，否则在输入文件名时需要用将文件名放在双引号中或者通过`\`对空格进行转义。
2. 扩展名：在Linux系统下文件的扩展名是可选的，但是使用扩展名有助于对文件内容的理解。有些应用程序要通过扩展名来识别文件，但是更多的应用程序并不依赖文件的扩展名，就像`file`命令在识别文件时并不是依据扩展名来判定文件的类型。
3. 隐藏文件：以点开头的文件在Linux系统中是隐藏文件（不可见文件）。

#### 访问权限

1. **chmod** - 改变文件模式比特。

    ```
    [root ~]# ls -l...-rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html...[root ~]# chmod g+w,o+w sohu.html[root ~]# ls -l...-rw-rw-rw-  1 root       root 211878 Jun 19 16:06 sohu.html...[root ~]# chmod 644 sohu.html[root ~]# ls -l...-rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html...
    ```

    > 说明：通过上面的例子可以看出，用`chmod`改变文件模式比特有两种方式：一种是字符设定法，另一种是数字设定法。除了`chmod`之外，可以通过`umask`来设定哪些权限将在新文件的默认权限中被删除。

    长格式查看目录或文件时显示结果及其对应权限的数值如下表所示。

    [![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day31-35/res/file-mode.png)](https://github.com/jackfrued/Python-100-Days/blob/master/Day31-35/res/file-mode.png)

2. **chown** - 改变文件所有者。

    ```
    [root ~]# ls -l...-rw-r--r--  1 root root     54 Jun 20 10:06 readme.txt...[root ~]# chown hellokitty readme.txt[root ~]# ls -l...-rw-r--r--  1 hellokitty root     54 Jun 20 10:06 readme.txt...
    ```

3. **chgrp** - 改变用户组。

#### 磁盘管理

1. 列出文件系统的磁盘使用状况 - **df**。

    ```
    [root ~]# df -hFilesystem      Size  Used Avail Use% Mounted on/dev/vda1        40G  5.0G   33G  14% /devtmpfs        486M     0  486M   0% /devtmpfs           497M     0  497M   0% /dev/shmtmpfs           497M  356K  496M   1% /runtmpfs           497M     0  497M   0% /sys/fs/cgrouptmpfs           100M     0  100M   0% /run/user/0
    ```

2. 磁盘分区表操作 - **fdisk**。

    ```
    [root ~]# fdisk -lDisk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectorsUnits = sectors of 1 * 512 = 512 bytesSector size (logical/physical): 512 bytes / 512 bytesI/O size (minimum/optimal): 512 bytes / 512 bytesDisk label type: dosDisk identifier: 0x000a42f4   Device Boot      Start         End      Blocks   Id  System/dev/vda1   *        2048    83884031    41940992   83  LinuxDisk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectorsUnits = sectors of 1 * 512 = 512 bytesSector size (logical/physical): 512 bytes / 512 bytesI/O size (minimum/optimal): 512 bytes / 512 bytes
    ```

3. 磁盘分区工具 - **parted**。

4. 格式化文件系统 - **mkfs**。

    ```
    [root ~]# mkfs -t ext4 -v /dev/sdb
    ```

    - `-t` - 指定文件系统的类型。
    - `-c` - 创建文件系统时检查磁盘损坏情况。
    - `-v` - 显示详细信息。

5. 文件系统检查 - **fsck**。

6. 转换或拷贝文件 - **dd**。

7. 挂载/卸载 - **mount** / **umount**。

8. 创建/激活/关闭交换分区 - **mkswap** / **swapon** / **swapoff**。

> **说明**：执行上面这些命令会带有一定的风险，如果不清楚这些命令的用法，最好不用随意使用，在使用的过程中，最好对照参考资料进行操作，并在操作前确认是否要这么做。

### 软件安装和配置

#### 使用包管理工具

1. yum

      

    \- Yellowdog Updater Modified。

    - `yum search`：搜索软件包，例如`yum search nginx`。
    - `yum list installed`：列出已经安装的软件包，例如`yum list installed | grep zlib`。
    - `yum install`：安装软件包，例如`yum install nginx`。
    - `yum remove`：删除软件包，例如`yum remove nginx`。
    - `yum update`：更新软件包，例如`yum update`可以更新所有软件包，而`yum update tar`只会更新tar。
    - `yum check-update`：检查有哪些可以更新的软件包。
    - `yum info`：显示软件包的相关信息，例如`yum info nginx`。

2. rpm

      

    \- Redhat Package Manager。

    - 安装软件包：`rpm -ivh <packagename>.rpm`。
    - 移除软件包：`rpm -e <packagename>`。
    - 查询软件包：`rpm -qa`，例如可以用`rpm -qa | grep mysql`来检查是否安装了MySQL相关的软件包。

下面以Nginx为例，演示如何使用yum安装软件。

```
[root ~]# yum -y install nginx...Installed:  nginx.x86_64 1:1.12.2-2.el7Dependency Installed:  nginx-all-modules.noarch 1:1.12.2-2.el7  nginx-mod-http-geoip.x86_64 1:1.12.2-2.el7  nginx-mod-http-image-filter.x86_64 1:1.12.2-2.el7  nginx-mod-http-perl.x86_64 1:1.12.2-2.el7  nginx-mod-http-xslt-filter.x86_64 1:1.12.2-2.el7  nginx-mod-mail.x86_64 1:1.12.2-2.el7  nginx-mod-stream.x86_64 1:1.12.2-2.el7Complete![root ~]# yum info nginxLoaded plugins: fastestmirrorLoading mirror speeds from cached hostfileInstalled PackagesName        : nginxArch        : x86_64Epoch       : 1Version     : 1.12.2Release     : 2.el7Size        : 1.5 MRepo        : installedFrom repo   : epelSummary     : A high performance web server and reverse proxy serverURL         : http://nginx.org/License     : BSDDescription : Nginx is a web server and a reverse proxy server for HTTP, SMTP, POP3 and            : IMAP protocols, with a strong focus on high concurrency, performance and low            : memory usage.[root ~]# nginx -vnginx version: nginx/1.12.2
```

移除Nginx。

```
[root ~]# yum -y remove nginx
```

下面以MySQL为例，演示如何使用rpm安装软件。要安装MySQL需要先到[MySQL官方网站](https://www.mysql.com/)下载对应的[RPM文件](https://dev.mysql.com/downloads/mysql/)，当然要选择和你使用的Linux系统对应的版本。MySQL现在是Oracle公司旗下的产品，在MySQL被收购后，MySQL的作者重新制作了一个MySQL的分支MariaDB，可以通过yum进行安装。

```
[root mysql]# lsmysql-community-client-5.7.22-1.el7.x86_64.rpmmysql-community-common-5.7.22-1.el7.x86_64.rpmmysql-community-libs-5.7.22-1.el7.x86_64.rpmmysql-community-server-5.7.22-1.el7.x86_64.rpm[root mysql]# yum -y remove mariadb-libs[root mysql]# yum -y install libaio[root mysql]#rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm...[root mysql]#rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm...[root mysql]#rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm...[root mysql]#rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm...
```

> 说明：由于MySQL和[MariaDB](https://mariadb.org/)的底层依赖库是有冲突的，所以上面我们首先用`yum`移除了名为mariadb-libs的依赖库并安装了名为libaio支持异步I/O操作的依赖库。关于MySQL和MariaDB之间的关系，可以阅读[维基百科](https://zh.wikipedia.org/wiki/MariaDB)上关于MariaDB的介绍。

移除安装的MySQL。

```
[root ~]# rpm -qa | grep mysql | xargs rpm -e
```

#### 下载解压配置环境变量

下面以安装MongoDB为例，演示这类软件应该如何安装。

```
[root ~]# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz--2018-06-21 18:32:53--  https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgzResolving fastdl.mongodb.org (fastdl.mongodb.org)... 52.85.83.16, 52.85.83.228, 52.85.83.186, ...Connecting to fastdl.mongodb.org (fastdl.mongodb.org)|52.85.83.16|:443... connected.HTTP request sent, awaiting response... 200 OKLength: 100564462 (96M) [application/x-gzip]Saving to: ‘mongodb-linux-x86_64-rhel70-3.6.5.tgz’100%[==================================================>] 100,564,462  630KB/s   in 2m 9s2018-06-21 18:35:04 (760 KB/s) - ‘mongodb-linux-x86_64-rhel70-3.6.5.tgz’ saved [100564462/100564462][root ~]# gunzip mongodb-linux-x86_64-rhel70-3.6.5.tgz[root ~]# tar -xvf mongodb-linux-x86_64-rhel70-3.6.5.tarmongodb-linux-x86_64-rhel70-3.6.5/READMEmongodb-linux-x86_64-rhel70-3.6.5/THIRD-PARTY-NOTICESmongodb-linux-x86_64-rhel70-3.6.5/MPL-2mongodb-linux-x86_64-rhel70-3.6.5/GNU-AGPL-3.0mongodb-linux-x86_64-rhel70-3.6.5/bin/mongodumpmongodb-linux-x86_64-rhel70-3.6.5/bin/mongorestoremongodb-linux-x86_64-rhel70-3.6.5/bin/mongoexportmongodb-linux-x86_64-rhel70-3.6.5/bin/mongoimportmongodb-linux-x86_64-rhel70-3.6.5/bin/mongostatmongodb-linux-x86_64-rhel70-3.6.5/bin/mongotopmongodb-linux-x86_64-rhel70-3.6.5/bin/bsondumpmongodb-linux-x86_64-rhel70-3.6.5/bin/mongofilesmongodb-linux-x86_64-rhel70-3.6.5/bin/mongoreplaymongodb-linux-x86_64-rhel70-3.6.5/bin/mongoperfmongodb-linux-x86_64-rhel70-3.6.5/bin/mongodmongodb-linux-x86_64-rhel70-3.6.5/bin/mongosmongodb-linux-x86_64-rhel70-3.6.5/bin/mongomongodb-linux-x86_64-rhel70-3.6.5/bin/install_compass[root ~]# vim .bash_profile...PATH=$PATH:$HOME/bin:$HOME/mongodb-linux-x86_64-rhel70-3.6.5/binexport PATH...[root ~]# source .bash_profile[root ~]# mongod --versiondb version v3.6.5git version: a20ecd3e3a174162052ff99913bc2ca9a839d618OpenSSL version: OpenSSL 1.0.1e-fips 11 Feb 2013allocator: tcmallocmodules: nonebuild environment:    distmod: rhel70    distarch: x86_64    target_arch: x86_64[root ~]# mongo --versionMongoDB shell version v3.6.5git version: a20ecd3e3a174162052ff99913bc2ca9a839d618OpenSSL version: OpenSSL 1.0.1e-fips 11 Feb 2013allocator: tcmallocmodules: nonebuild environment:    distmod: rhel70    distarch: x86_64    target_arch: x86_64
```

> 说明：当然也可以通过yum来安装MongoDB，具体可以参照[官方网站](https://docs.mongodb.com/master/administration/install-on-linux/)上给出的说明。

#### 源代码构建安装

1. 安装Python 3.6。

    ```
    [root ~]# yum install gcc[root ~]# wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz[root ~]# gunzip Python-3.6.5.tgz[root ~]# tar -xvf Python-3.6.5.tar[root ~]# cd Python-3.6.5[root ~]# ./configure --prefix=/usr/local/python36 --enable-optimizations[root ~]# yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel[root ~]# make && make install...[root ~]# ln -s /usr/local/python36/bin/python3.6 /usr/bin/python3[root ~]# python3 --versionPython 3.6.5[root ~]# python3 -m pip install -U pip[root ~]# pip3 --version
    ```

    > 说明：上面在安装好Python之后还需要注册PATH环境变量，将Python安装路径下bin文件夹的绝对路径注册到PATH环境变量中。注册环境变量可以修改用户主目录下的.bash_profile或者/etc目录下的profile文件，二者的区别在于前者相当于是用户环境变量，而后者相当于是系统环境变量。

2. 安装Redis-3.2.12。

    ```
    [root ~]# wget http://download.redis.io/releases/redis-3.2.12.tar.gz[root ~]# gunzip redis-3.2.12.tar.gz[root ~]# tar -xvf redis-3.2.12.tar[root ~]# cd redis-3.2.12[root ~]# make && make install[root ~]# redis-server --versionRedis server v=3.2.12 sha=00000000:0 malloc=jemalloc-4.0.3 bits=64 build=5bc5cd3c03d6ceb6[root ~]# redis-cli --versionredis-cli 3.2.12
    ```

### 配置服务

我们可以Linux系统下安装和配置各种服务，也就是说我们可以把Linux系统打造成数据库服务器、Web服务器、缓存服务器、文件服务器、消息队列服务器等等。Linux下的大多数服务都被设置为守护进程（驻留在系统后台运行，但不会因为服务还在运行而导致Linux无法停止运行），所以我们安装的服务通常名字后面都有一个字母`d`，它是英文单词`daemon`的缩写，例如：防火墙服务叫firewalld，我们之前安装的MySQL服务叫mysqld，Apache服务器叫httpd等。在安装好服务之后，可以使用`systemctl`命令或`service`命令来完成对服务的启动、停止等操作，具体操作如下所示。

1. 启动防火墙服务。

    ```
    [root ~]# systemctl start firewalld
    ```

2. 终止防火墙服务。

    ```
    [root ~]# systemctl stop firewalld
    ```

3. 重启防火墙服务。

    ```
    [root ~]# systemctl restart firewalld
    ```

4. 查看防火墙服务状态。

    ```
    [root ~]# systemctl status firewalld
    ```

5. 设置/禁用防火墙服务开机自启。

    ```
    [root ~]# systemctl enable firewalldCreated symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.[root ~]# systemctl disable firewalldRemoved symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
    ```

### 计划任务

1. 在指定的时间执行命令。

    - **at** - 将任务排队，在指定的时间执行。
    - **atq** - 查看待执行的任务队列。
    - **atrm** - 从队列中删除待执行的任务。

    指定3天以后下午5点要执行的任务。

    ```
    [root ~]# at 5pm+3daysat> rm -f /root/*.htmlat> <EOT>job 9 at Wed Jun  5 17:00:00 2019
    ```

    查看待执行的任务队列。

    ```
    [root ~]# atq9       Wed Jun  5 17:00:00 2019 a root
    ```

    从队列中删除指定的任务。

    ```
    [root ~]$ atrm 9
    ```

2. 计划任务表 - **crontab**。

    ```
    [root ~]# crontab -e* * * * * echo "hello, world!" >> /root/hello.txt59 23 * * * rm -f /root/*.log
    ```

    > 说明：输入`crontab -e`命令会打开vim来编辑Cron表达式并指定触发的任务，上面我们定制了两个计划任务，一个是每分钟向/root目录下的hello.txt中追加输出`hello, world!`；另一个是每天23时59分执行删除/root目录下以log为后缀名的文件。如果不知道Cron表达式如何书写，可以参照/etc/crontab文件中的提示（下面会讲到）或者用搜索引擎找一下“Cron表达式在线生成器”来生成Cron表达式。

    和crontab相关的文件在`/etc`目录下，通过修改`/etc`目录下的crontab文件也能够定制计划任务。

    ```
    [root ~]# cd /etc[root etc]# ls -l | grep cron-rw-------.  1 root root      541 Aug  3  2017 anacrontabdrwxr-xr-x.  2 root root     4096 Mar 27 11:56 cron.ddrwxr-xr-x.  2 root root     4096 Mar 27 11:51 cron.daily-rw-------.  1 root root        0 Aug  3  2017 cron.denydrwxr-xr-x.  2 root root     4096 Mar 27 11:50 cron.hourlydrwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.monthly-rw-r--r--   1 root root      493 Jun 23 15:09 crontabdrwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.weekly[root etc]# vim crontab  1 SHELL=/bin/bash  2 PATH=/sbin:/bin:/usr/sbin:/usr/bin  3 MAILTO=root  4  5 # For details see man 4 crontabs  6  7 # Example of job definition:  8 # .---------------- minute (0 - 59)  9 # |  .------------- hour (0 - 23) 10 # |  |  .---------- day of month (1 - 31) 11 # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ... 12 # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat 13 # |  |  |  |  | 14 # *  *  *  *  * user-name  command to be executed
    ```

### 网络访问和管理

1. 安全远程连接 - **ssh**。

    ```
    [root ~]$ ssh root@120.77.222.217The authenticity of host '120.77.222.217 (120.77.222.217)' can't be established.ECDSA key fingerprint is SHA256:BhUhykv+FvnIL03I9cLRpWpaCxI91m9n7zBWrcXRa8w.ECDSA key fingerprint is MD5:cc:85:e9:f0:d7:07:1a:26:41:92:77:6b:7f:a0:92:65.Are you sure you want to continue connecting (yes/no)? yesWarning: Permanently added '120.77.222.217' (ECDSA) to the list of known hosts.root@120.77.222.217's password: 
    ```

2. 通过网络获取资源 - **wget**。

    - -b 后台下载模式
    - -O 下载到指定的目录
    - -r 递归下载

3. 发送和接收邮件 - **mail**。

4. 网络配置工具（旧） - **ifconfig**。

    ```
    [root ~]# ifconfig eth0eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500        inet 172.18.61.250  netmask 255.255.240.0  broadcast 172.18.63.255        ether 00:16:3e:02:b6:46  txqueuelen 1000  (Ethernet)        RX packets 1067841  bytes 1296732947 (1.2 GiB)        RX errors 0  dropped 0  overruns 0  frame 0        TX packets 409912  bytes 43569163 (41.5 MiB)        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 
    ```

5. 网络配置工具（新） - **ip**。

    ```
    [root ~]# ip address1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00    inet 127.0.0.1/8 scope host lo       valid_lft forever preferred_lft forever2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000    link/ether 00:16:3e:02:b6:46 brd ff:ff:ff:ff:ff:ff    inet 172.18.61.250/20 brd 172.18.63.255 scope global eth0       valid_lft forever preferred_lft forever
    ```

6. 网络可达性检查 - **ping**。

    ```
    [root ~]# ping www.baidu.com -c 3PING www.a.shifen.com (220.181.111.188) 56(84) bytes of data.64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=1 ttl=51 time=36.3 ms64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=2 ttl=51 time=36.4 ms64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=3 ttl=51 time=36.4 ms--- www.a.shifen.com ping statistics ---3 packets transmitted, 3 received, 0% packet loss, time 2002msrtt min/avg/max/mdev = 36.392/36.406/36.427/0.156 ms
    ```

7. 显示或管理路由表 - **route**。

8. 查看网络服务和端口 - **netstat** / **ss**。

    ```
    [root ~]# netstat -nap | grep nginx
    ```

9. 网络监听抓包 - **tcpdump**。

10. 安全文件拷贝 - **scp**。

```
[root ~]# scp root@1.2.3.4:/root/guido.jpg hellokitty@4.3.2.1:/home/hellokitty/pic.jpg
```

1. 文件同步工具 - **rsync**。

    > 说明：使用`rsync`可以实现文件的自动同步，这个对于文件服务器来说相当重要。关于这个命令的用法，我们在后面讲项目部署的时候为大家详细说明。

2. 安全文件传输 - **sftp**。

    ```
    [root ~]# sftp root@1.2.3.4root@1.2.3.4's password:Connected to 1.2.3.4.sftp>
    ```

    - `help`：显示帮助信息。
    - `ls`/`lls`：显示远端/本地目录列表。
    - `cd`/`lcd`：切换远端/本地路径。
    - `mkdir`/`lmkdir`：创建远端/本地目录。
    - `pwd`/`lpwd`：显示远端/本地当前工作目录。
    - `get`：下载文件。
    - `put`：上传文件。
    - `rm`：删除远端文件。
    - `bye`/`exit`/`quit`：退出sftp。

### 进程管理

1. 查看进程 - **ps**。

    ```
    [root ~]# ps -efUID        PID  PPID  C STIME TTY          TIME CMDroot         1     0  0 Jun23 ?        00:00:05 /usr/lib/systemd/systemd --switched-root --system --deserialize 21root         2     0  0 Jun23 ?        00:00:00 [kthreadd]...[root ~]# ps -ef | grep mysqldroot      4943  4581  0 22:45 pts/0    00:00:00 grep --color=auto mysqldmysql    25257     1  0 Jun25 ?        00:00:39 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
    ```

2. 显示进程状态树 - **pstree**。

    ```
    [root ~]# pstreesystemd─┬─AliYunDun───18*[{AliYunDun}]        ├─AliYunDunUpdate───3*[{AliYunDunUpdate}]        ├─2*[agetty]        ├─aliyun-service───2*[{aliyun-service}]        ├─atd        ├─auditd───{auditd}        ├─dbus-daemon        ├─dhclient        ├─irqbalance        ├─lvmetad        ├─mysqld───28*[{mysqld}]        ├─nginx───2*[nginx]        ├─ntpd        ├─polkitd───6*[{polkitd}]        ├─rsyslogd───2*[{rsyslogd}]        ├─sshd───sshd───bash───pstree        ├─systemd-journal        ├─systemd-logind        ├─systemd-udevd        └─tuned───4*[{tuned}]
    ```

3. 查找与指定条件匹配的进程 - **pgrep**。

    ```
    [root ~]$ pgrep mysqld3584
    ```

4. 通过进程号终止进程 - **kill**。

    ```
    [root ~]$ kill -l 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR111) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+338) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+843) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+1348) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-1253) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-758) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-263) SIGRTMAX-1  64) SIGRTMAX[root ~]# kill 1234[root ~]# kill -9 1234
    ```

    例子：用一条命令强制终止正在运行的Redis进程。

    ```
    ps -ef | grep redis | grep -v grep | awk '{print $2}' | xargs kill
    ```

5. 通过进程名终止进程 - **killall** / **pkill**。

    结束名为mysqld的进程。

    ```
    [root ~]# pkill mysqld
    ```

    结束hellokitty用户的所有进程。

    ```
    [root ~]# pkill -u hellokitty
    ```

    > 说明：这样的操作会让hellokitty用户和服务器断开连接。

6. 将进程置于后台运行。

    - `Ctrl+Z` - 快捷键，用于停止进程并置于后台。
    - `&` - 将进程置于后台运行。

    ```
    [root ~]# mongod &[root ~]# redis-server...^Z[4]+  Stopped                 redis-server
    ```

7. 查询后台进程 - **jobs**。

    ```
    [root ~]# jobs[2]   Running                 mongod &[3]-  Stopped                 cat[4]+  Stopped                 redis-server
    ```

8. 让进程在后台继续运行 - **bg**。

    ```
    [root ~]# bg %4[4]+ redis-server &[root ~]# jobs[2]   Running                 mongod &[3]+  Stopped                 cat[4]-  Running                 redis-server &
    ```

9. 将后台进程置于前台 - **fg**。

    ```
    [root ~]# fg %4redis-server
    ```

    > 说明：置于前台的进程可以使用`Ctrl+C`来终止它。

10. 调整程序/进程运行时优先级 - **nice** / **renice**。

11. 用户登出后进程继续工作 - **nohup**。

    ```
    [root ~]# nohup ping www.baidu.com > result.txt &
    ```

12. 跟踪进程系统调用情况 - **strace**。

    ```
    [root ~]# pgrep mysqld8803[root ~]# strace -c -p 8803strace: Process 8803 attached^Cstrace: Process 8803 detached% time     seconds  usecs/call     calls    errors syscall------ ----------- ----------- --------- --------- ---------------- 99.18    0.005719        5719         1           restart_syscall  0.49    0.000028          28         1           mprotect  0.24    0.000014          14         1           clone  0.05    0.000003           3         1           mmap  0.03    0.000002           2         1           accept------ ----------- ----------- --------- --------- ----------------100.00    0.005766                     5           total
    ```

    > 说明：这个命令的用法和参数都比较复杂，建议大家在真正用到这个命令的时候再根据实际需要进行了解。

13. 查看当前运行级别 - **runlevel**。

    ```
    [root ~]# runlevelN 3
    ```

14. 实时监控进程占用资源状况 - **top**。

    ```
    [root ~]# toptop - 23:04:23 up 3 days, 14:10,  1 user,  load average: 0.00, 0.01, 0.05Tasks:  65 total,   1 running,  64 sleeping,   0 stopped,   0 zombie%Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 stKiB Mem :  1016168 total,   191060 free,   324700 used,   500408 buff/cacheKiB Swap:        0 total,        0 free,        0 used.   530944 avail Mem...
    ```

    - `-c` - 显示进程的整个路径。
    - `-d` - 指定两次刷屏之间的间隔时间（秒为单位）。
    - `-i` - 不显示闲置进程或僵尸进程。
    - `-p` - 显示指定进程的信息。

### 系统诊断

1. 系统启动异常诊断 - **dmesg**。

2. 查看系统活动信息 - **sar**。

    ```
    [root ~]# sar -u -r 5 10Linux 3.10.0-957.10.1.el7.x86_64 (izwz97tbgo9lkabnat2lo8z)      06/02/2019      _x86_64_        (2 CPU)06:48:30 PM     CPU     %user     %nice   %system   %iowait    %steal     %idle06:48:35 PM     all      0.10      0.00      0.10      0.00      0.00     99.8006:48:30 PM kbmemfree kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty06:48:35 PM   1772012   2108392     54.33    102816   1634528    784940     20.23    793328   1164704         0
    ```

    - `-A` - 显示所有设备（CPU、内存、磁盘）的运行状况。
    - `-u` - 显示所有CPU的负载情况。
    - `-d` - 显示所有磁盘的使用情况。
    - `-r` - 显示内存的使用情况。
    - `-n` - 显示网络运行状态。

3. 查看内存使用情况 - **free**。

    ```
    [root ~]# free              total        used        free      shared  buff/cache   availableMem:        1016168      323924      190452         356      501792      531800Swap:             0           0           0
    ```

4. 虚拟内存统计 - **vmstat**。

    ```
    [root ~]# vmstatprocs -----------memory---------- ---swap-- -----io---- -system-- ------cpu----- r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st 2  0      0 204020  79036 667532    0    0     5    18  101   58  1  0 99  0  0
    ```

5. CPU信息统计 - **mpstat**。

    ```
    [root ~]# mpstatLinux 3.10.0-957.5.1.el7.x86_64 (iZ8vba0s66jjlfmo601w4xZ)       05/30/2019      _x86_64_        (1 CPU)01:51:54 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle01:51:54 AM  all    0.71    0.00    0.17    0.04    0.00    0.00    0.00    0.00    0.00   99.07
    ```

6. 查看进程使用内存状况 - **pmap**。

    ```
    [root ~]# ps  PID TTY          TIME CMD 4581 pts/0    00:00:00 bash 5664 pts/0    00:00:00 ps[root ~]# pmap 45814581:   -bash0000000000400000    884K r-x-- bash00000000006dc000      4K r---- bash00000000006dd000     36K rw--- bash00000000006e6000     24K rw---   [ anon ]0000000001de0000    400K rw---   [ anon ]00007f82fe805000     48K r-x-- libnss_files-2.17.so00007f82fe811000   2044K ----- libnss_files-2.17.so...
    ```

7. 报告设备CPU和I/O统计信息 - **iostat**。

    ```
    [root ~]# iostatLinux 3.10.0-693.11.1.el7.x86_64 (iZwz97tbgo9lkabnat2lo8Z)      06/26/2018      _x86_64_       (1 CPU)avg-cpu:  %user   %nice %system %iowait  %steal   %idle           0.79    0.00    0.20    0.04    0.00   98.97Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtnvda               0.85         6.78        21.32    2106565    6623024vdb               0.00         0.01         0.00       2088          0
    ```

8. 显示所有PCI设备 - **lspci**。

    ```
    [root ~]# lspci00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]00:01.1 IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]00:01.2 USB controller: Intel Corporation 82371SB PIIX3 USB [Natoma/Triton II] (rev 01)00:01.3 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 03)00:02.0 VGA compatible controller: Cirrus Logic GD 544600:03.0 Ethernet controller: Red Hat, Inc. Virtio network device00:04.0 Communication controller: Red Hat, Inc. Virtio console00:05.0 SCSI storage controller: Red Hat, Inc. Virtio block device00:06.0 SCSI storage controller: Red Hat, Inc. Virtio block device00:07.0 Unclassified device [00ff]: Red Hat, Inc. Virtio memory balloon
    ```

9. 显示进程间通信设施的状态 - **ipcs**。

    ```
    [root ~]# ipcs------ Message Queues --------key        msqid      owner      perms      used-bytes   messages    ------ Shared Memory Segments --------key        shmid      owner      perms      bytes      nattch     status      ------ Semaphore Arrays --------key        semid      owner      perms      nsems
    ```

### Shell编程

之前我们提到过，Shell是一个连接用户和操作系统的应用程序，它提供了人机交互的界面（接口），用户通过这个界面访问操作系统内核的服务。Shell脚本是一种为Shell编写的脚本程序，我们可以通过Shell脚本来进行系统管理，同时也可以通过它进行文件操作。总之，编写Shell脚本对于使用Linux系统的人来说，应该是一项标配技能。

互联网上有大量关于Shell脚本的相关知识，我不打算再此对Shell脚本做一个全面系统的讲解，我们通过下面的代码来感性的认识下Shell脚本就行了。

例子1：输入两个整数m和n，计算从m到n的整数求和的结果。

```
#!/usr/bin/bashprintf 'm = 'read mprintf 'n = 'read na=$msum=0while [ $a -le $n ]do    sum=$[ sum + a ]    a=$[ a + 1 ]doneecho '结果: '$sum
```

例子2：自动创建文件夹和指定数量的文件。

```
#!/usr/bin/bashprintf '输入文件夹名: 'read dirprintf '输入文件名: 'read fileprintf '输入文件数量(<1000): 'read numif [ $num -ge 1000 ]then    echo '文件数量不能超过1000'else    if [ -e $dir -a -d $dir ]    then        rm -rf $dir    else        if [ -e $dir -a -f $dir ]        then            rm -f $dir        fi    fi    mkdir -p $dir    index=1    while [ $index -le $num ]    do        if [ $index -lt 10 ]        then            pre='00'        elif [ $index -lt 100 ]        then            pre='0'        else            pre=''        fi        touch $dir'/'$file'_'$pre$index        index=$[ index + 1 ]    donefi
```

例子3：自动安装指定版本的Redis。

```
#!/usr/bin/bashinstall_redis() {    if ! which redis-server > /dev/null    then        cd /root        wget $1$2'.tar.gz' >> install.log        gunzip /root/$2'.tar.gz'        tar -xf /root/$2'.tar'        cd /root/$2        make >> install.log        make install >> install.log        echo '安装完成'    else        echo '已经安装过Redis'    fi}install_redis 'http://download.redis.io/releases/' $1
```

### 相关资源

1. Linux命令行常用快捷键

    | 快捷键     | 功能说明                                     |
    | ---------- | -------------------------------------------- |
    | tab        | 自动补全命令或路径                           |
    | Ctrl+a     | 将光标移动到命令行行首                       |
    | Ctrl+e     | 将光标移动到命令行行尾                       |
    | Ctrl+f     | 将光标向右移动一个字符                       |
    | Ctrl+b     | 将光标向左移动一个字符                       |
    | Ctrl+k     | 剪切从光标到行尾的字符                       |
    | Ctrl+u     | 剪切从光标到行首的字符                       |
    | Ctrl+w     | 剪切光标前面的一个单词                       |
    | Ctrl+y     | 复制剪切命名剪切的内容                       |
    | Ctrl+c     | 中断正在执行的任务                           |
    | Ctrl+h     | 删除光标前面的一个字符                       |
    | Ctrl+d     | 退出当前命令行                               |
    | Ctrl+r     | 搜索历史命令                                 |
    | Ctrl+g     | 退出历史命令搜索                             |
    | Ctrl+l     | 清除屏幕上所有内容在屏幕的最上方开启一个新行 |
    | Ctrl+s     | 锁定终端使之暂时无法输入内容                 |
    | Ctrl+q     | 退出终端锁定                                 |
    | Ctrl+z     | 将正在终端执行的任务停下来放到后台           |
    | !!         | 执行上一条命令                               |
    | !数字      | 执行数字对应的历史命令                       |
    | !字母      | 执行最近的以字母打头的命令                   |
    | !$ / Esc+. | 获得上一条命令最后一个参数                   |
    | Esc+b      | 移动到当前单词的开头                         |
    | Esc+f      | 移动到当前单词的结尾                         |

2. man查阅命令手册的内容说明

    | 手册中的标题 | 功能说明                                                     |
    | ------------ | ------------------------------------------------------------ |
    | NAME         | 命令的说明和介绍                                             |
    | SYNOPSIS     | 使用该命令的基本语法                                         |
    | DESCRIPTION  | 使用该命令的详细描述，各个参数的作用，有时候这些信息会出现在OPTIONS中 |
    | OPTIONS      | 命令相关参数选项的说明                                       |
    | EXAMPLES     | 使用该命令的参考例子                                         |
    | EXIT STATUS  | 命令结束的退出状态码，通常0表示成功执行                      |
    | SEE ALSO     | 和命令相关的其他命令或信息                                   |
    | BUGS         | 和命令相关的缺陷的描述                                       |
    | AUTHOR       | 该命令的作者介绍                                             |





##### 目录详解

在根目录下有许多目录，包含不同功能的文件

```
/bin : 二进制文件，存放指令/boot : 存放和启动相关的内容/dev : 存放设备的地方/etc : 存放配置文件/home : 普通用户家目录/lib  /lib64 : 存放都是库文件lost + found : linux系统文件独有的一个目录/media : 媒体设备/mnt : 设备挂载的地方/opt : 可选的附加程序/proc : 和进程相关的文件/root : 超级用户的家目录（）/sbin : 只有超级管理员才能执行的指令/selinux : 一种安全机制，基本没用，还得关掉它/srv : 存放相关服务文件/sys : 存放硬件相关驱动信息/tmp : 存放临时文件/usr : unix系统资源, 手动安装软件时要安装到 /usr/local里面/var : 存放日志、数据库等
```

##### 家目录

**Linux系统中，每个用户都会有家目录，都用 ~ 表示，但表示的路径却不一样。**

超级用户的家目录 ~ 的路径是：/root

普通用户的家目录 ~ 的路径是：/home/用户名

**注意：任何用户登录Linux系统后，起始位置都在是自己的家目录路径下。**

##### 隐藏类型

**在linux中，以 . 开头的文件或文件夹就属于隐藏类型。**

**注意：ls命令查看不到隐藏类型，ls -a命令能查看到。**

```
.     .autofsck    .ssh
```

### 系统基本操作

##### 登录系统

**坑：这里不要用小键盘（数字键盘）来输入密码，因为你不确定num lock（数字锁）是否打开。假如打开了键盘锁，进行了输入，输入的密码虽然不会有任何显示的，但还是会有内容的输入，只不过不是数字。**

```
1.启动或连接Linux系统2.出现login3.输入用户名（管理员为root）和密码4.敲enter进入系统
```

##### 路径命令

**绝对路径**: 相对于根目录的路径
**相对路径**: 相对于当前目录的路径

```
pwd : 当前目录的绝对路径# 注意：cd命令中，在cd后面都要带一个空格。cd .. : 返回上一级目录cd 目录路径 : 切换目录(目录就是文件夹)cd / : 根目录cd ~ : 当前用户的家目录(快捷键cd，因为cd == cd ~)   cd - : 返回上一个目录(注意：是上个目录，不是上级目录)
```

##### 退出系统

```
exit : 退出系统登录logout : 退出登录
```

### 远程连接

**注意：这里针对的是虚拟机，如果是购买的服务器，记住服务器的公网IP就行了。**

##### 虚拟机配置

Workstation——虚拟机——设置——网络适配器——NAT模式——确定

##### ssh

ssh是一个远程登录协议，默认端口号是22

```
yum install sshd-service  # 安装sshd服务
```

配置ssh

```
vim /etc/ssh/sshd_config
```

编辑内容为：

```
Port 22					# 端口号22Protocol 2				# ssh2类型PermitRootLogin yes	    # 允许任何类型登录
```

PermitRootLogin可以限定root用户通过ssh的登录方式，如禁止登陆、禁止密码登录、仅允许密钥登陆和开放登陆，以下是对可选项的概括：

| 参数类别             | ssh登陆 | 登录方式       | 交互shell          |
| -------------------- | ------- | -------------- | ------------------ |
| yes                  | 允许    | 没有限制       | 没有限制           |
| without-password     | 允许    | 除密码以外     | 没有限制           |
| forced-commands-only | 允许    | 仅允许使用密钥 | 仅允许已授权的命令 |
| no                   | 不允许  | N/A            | N/A                |

启动ssh服务

```
service sshd status		  # 查看sshd服务状态service sshd start		  # 启动sshd服务service sshd restart      # 重启sshd服务service sshd stop		  # 停止sshd服务
```

##### 配置IP

执行`ifconfig`命令，记录eth0中网卡MAC地址，即`HWaddr`的值

编辑ifcfg-eth0配置文件

```
vim /etc/sysconfig/network-scripts/ifcfg-eth0 
```

内容为：

**注意：这里设置的IP不能与虚拟网卡VirtualBox、VMnet1、VMnet8中的IP起冲突。**

```
DEVICE=eth0									# 设备名称eth0BOOTPROTO=static							# 地址类型静态HWADDR=00:50:56:2D:C7:70					# 上面记录的HWaddr的值TYPE=Ethernet								# 网络类型UUID=a003d5b9-f6c3-456c-b475-390bdc93f734	# 唯一标识ONBOOT=yes									# 自动加载NM_CONTROLLED=yes							# NNetwork Manager托管IPADDR=192.168.1.120						# IP地址NETMASK=255.255.255.0						# 子网掩码GATEWAY=192.168.1.1							# 网关
```

退出保存后，重启network

```
service network restart
```

##### Linux连接

ssh也是linux的一个指令，通过ssh可以实现linux1登录linux2。

```
# 登录格式 : ssh 用户名@ip地址		    ssh root@10.7.181.66   输入密码即可登录
```

##### Windows连接

使用windows登录linux就需要使用软件：Xshell

打开Xshell——文件——新建——名称（自定义）——协议（SSH）——主机（IP地址，虚拟机就是上面配置的IP地址，服务器就是他的公网IP地址）——端口号（22）——用户身份验证——方法（password）——用户名（登录Linux的名称）——密码（登录Linux的密码）——确定

### 用户系统

##### 运行级别

**系统运行级别就是系统使用的功能。**

```
cat /etc/inittab : 在文件中修改系统默认运行级别id:3:initdefault : 3就代表系统的运行默认级别init 3 : 设置当前系统运行级别为3    # 0:关机（不能设为默认级别）    # 1:单用户（安全模式）    # 2:不完全多用户，不能用网络    # 3:多用户    # 4:未分配    # 5:图形界面    # 6:重启（不能设为默认级别）runlevel：查看系统当前运行级别
```

##### 基本信息

```
超级用户root进入Linux系统：[root@localhost ~]#root : 超级管理员，拥有至高无上的权限localhost : 主机名~ : 代表的是当前用户的家目录，也表示当前所在位置# : 代表的意思是超级管理员在执行指令普通用户bajie进入Linux系统:[bajie@localhost ~]$bajie : 用户名localhost : 主机名~ : 代表的是当前用户的家目录，也表示当前所在位置$ : 代表的是普通用户在执行指令
```

##### 管理用户

**Linux是一个多用户系统，可以多用户登录**

**坑：注意设置密码，不要使用小键盘。**

**注意：普通用户只能更改自己的密码，管理员可以更改所有人的密码。**

```
# 查看用户whoami : 查询自己是谁who : 查看登录用户（tty本地终端，pts远程终端）w : 查看登录用户详细信息（IDLE：未操作时间，what：执行的操作）# 增加用户useradd sc：添加用户sc（-u UID：手工指定用户的UID号，-G 组名：指定用户的附加组，-g 组名：指定用户的初始组，-c "说明"：添加说明，\：命令太长换行，修改新添加的用户）passwd sc：超级用户给sc用户设置密码（添加了用户，就要马上设置密码，否则该用户是不完整的。passwd直接回车就是自己设置自己的密码（普通用户、超级用户都可以））# 锁定、解锁passwd -l sc : 锁定sc用户，不能登录（这是因为在加密文件的密码前加了！，导致密码失效）passwd -u sc : 解锁sc用户# 修改用户信息usermod : 修改用户信息（-u UID：手工指定用户的UID号，-G 组名：指定用户的附加组，-L：临时锁定用户，-U：解锁用户，修改已存在的用户）chage : 修改用户密码状态（-l：列出用户的详细密码状态，-I 天数：密码过后宽限天数，-E 日期：账号失效时间，-d：修改密码最后一次更改日期）chage -d 0 lamp : 将lamp用户的密码修改日期归0，用户一登陆就要修改密码# 删除用户userdel -r 用户名 : 删除用户（-r：删除用户的同时删除用户家目录）# 切换用户su - user1 : 切换到user1（-：切换用户时，连带用户的环境变量一起切换。命令env就可以查看用户的环境变量）（超级用户切换到普通用户不需要密码，反向切换就要密码，普通用户切换为普通用户要密码）# 历史信息last：列出登陆过和在线的用户信息及系统重启信息lastlog：查看所有用户是否登录的信息lastlog -u 502：只查看502用户是否的登录信息
```

##### 管理组

**每个用户都有自己的所属组**

```
groupadd 组名 : 添加组groupmod 组名 : 修改组groupmod -n testrp group1 : 将组名group1改为testrpgroupdel 组名 : 删除组（组中存在用户，若组是用户的初始组，则不能删除；若是附加组，就能删除）gpasswd 组名 : 组中添加或删除用户（-a 用户名：向组中添加用户，-d 用户名：在组中删除用户；这些都是附加用户）id user1：查询user1用户id和组id和在哪些组当中
```

##### 用户配置文件

Linux中主要是通过用户配置文件按来查看和修改用户信息。

```
用户配置文件:/etc/passwd# 第一字段：用户名称（例：root、bin）# 第二字段：密码标志（x：用户存在密码（没有密码的用户只能本机登陆，不能远程登陆））# 第三字段：UID（0：超级用户，1-499：系统用户（伪用户，不能删除），500-65535：普通用户（将UID改为0，就能成为超级用户，改GID没有用））# 第四字段：GID（用户初始组ID）# 额外：初始组，用户登录就拥有这个组权限，用户创建就建立并属于同名的初始组，初始组只能有一个。	   附加组，用户可以加入多个其他的用户组，并拥有这些组的权限，附加组可以有多个。# 第五字段：用户说明# 第六字段：家目录（超级用户：/root/，普通用户：/home/用户名/）# 第七字段：登录之后的shell（shell是Linux的命令解释器）例子：root:x:0:0:root:/root:/bin/bash（超级用户）例子：ntp:x:38:38::/etc.ntp:sbin/nologin（伪用户，nologin禁止登录）例子：lampl:x:503:503::/home/lampl:bin/bash（普通用户，都是在bin/bash才能登陆执行权限，如果将bin/bash改为sbin/nologin就会禁止该用户登录）# 影子文件：/etc/shadow文件，用来存放加密的密码（只有root能查看）# 第一字段：用户名# 第二字段：加密密码（密码是!!或*代表没有密码，不能登陆）# 第三字段：密码最后一次修改日期（时间戳，1970年1月1号，一天加1）# 第四字段：两次密码的修改间隔时间（和第三字段比较）# 第五字段：密码有效期（和第三字段比较）# 第六字段：密码修改到期前的警告天数（和五字段相比）# 第七字段：密码过期的宽限天数（0：密码过期失效，-1：密码永不失效）# 第八字段：账号失效时间（账号有效期，过期失效，设置时间戳表示）# 第九字段：保留（暂时不用）# 时间戳换算为时间：date -d "1970-01-01 16076 days"# 时间换算为时间戳：echo $(($(date --date="2014/01/06" +%s)/86400+1))# 组信息文件：/etc/group（组影子文件：/etc/gshadow，保存组密码）# 第一字段：组名# 第二字段：组密码（x：存在组密码，一般不用）# 第三字段：GID（组的ID）# 第四字段：组中附加用户# 用户家目录# 超级用户：/root/，所有者和所属组都是root用户，权限是550# 普通用户：/home/用户名/，所有者和所属组都是此用户，权限是700（普通用户变为超级用户，家目录不会变）
```

### 文件命令

##### 查看、新建

```
ls : 显示当前目录里面的文件及文件夹
ls 目录路径 : 显示路径中目录下的文件及文件夹（路径，绝对、相对都可以）
ls -a : 显示当前目录里面所有文件，包含隐藏类型
ls -l : 列表形式显示文件的详细信息
	-rw-r--r--. 1 root root 3384 8月  28 2018 install.log.syslog
	drwxr-xr-x. 5 root root 4096 8月  31 2018 ziliao1
    第一列：类型，- : 文件，d : 目录，l : 链接，c : 字符设备，b : 块设备
    第二列-第十列：文件权限
    第十一列：没影响，不用管
    第十二列：如果是文件，代表的是硬链接的个数
    第十三列：所属用户   root
    第十四列：所属组     root
    第十五列：文件的大小  单位kb
    第十六列-第十八列：文件创建、修改时间
    第十九列：文件的名字
touch /tmp/love.list：在tmp文件夹下创建love.list文件
touch program files：在当前路径下创建文件program和文件files
touch "program files"：在当前路径下创建文件program files（不建议文件命名包含空格）
```

##### 复制、搜索

```
cp /etc/1.conf /tmp : 将1.conf文件复制到tmp目录下（复制文件）cp /etc/1.conf /etc/2.conf /tmp : 将1.conf和2.conf文件复制到tmp目录下（复制文件）cp -p /etc/1.conf /tmp : 将1.conf文件复制到tmp目录下（复制文件，包括文件的所有属性）find / -name *init* : 根目录搜索名称中包含init的文件（*匹配任意字符，？匹配单个字符）find /etc -name init : 在etc文件夹下搜索名称为init的文件（区分大小写，参数是-iname不区分大小写）find / -size +204800 : 在根目录下搜索大于100MB的文件（+n：大于n，-n：小于n，n是数据块，大小为0.5kB）find / -size +163840 -a -size -204800 : 根目录下搜索大于80MB小于100MB的文件（-a两个条件同时满足，-o满足一个条件即可）find / -name init* -a -type f：根目录下所搜以init开头的文件（-type类型，f文件，d文件夹，l软链接文件，-inum根据i节点查找）find /home -user shen：在根目录下搜索所有者为shen的文件（-group根据所属组搜索）find /etc -cmin -5：在etc下搜索5分钟内被修改过的属性的文件和目录（-mmin文件内容）find . -name init -exec ls -l {} \.：当前目录搜索名称为init的文件并显示详细信息（-exec表示对搜索结果的操作，ls -l显示详细信息，{} \.是固定格式）# locate是在资料库中查找，但不能查找新建文件，因为新建文件还没有添加到资料库里面，要查找新建文件，必须输入先命令updatedb来更新资料库（tmp临时文件不在更新范围内），再进行查找就能查找到。locate init：查找名称为init的文件（精确查找，区分大小写，添加参数-i就不区分大小写）which ls：查找ls命令所在的目录whereis rm：查找rm命令所在目录和帮助文档（和which差不多）grep mysql /root/install.log：在install.log中查找含有mysql的内容（-i不区分大小写）grep -v ^# /etc/init：查看init文件中不是#开头的文代码行（^以什么开头，#表示注释行）
```

### 网络命令

##### 消息命令

```
write shen：给用户shen发送信息（前提shen是登录状态，ctrl+D保存结束并发送）
wall hello：给所有在线用户发送一个内容为hello的信息。（广播信息）
```

##### 端口查看

```
netstat：显示网络相关信息（-l监听，-r路由，-n显示IP地址和端口号，-tuln查看监听端口，-an查看所有网络连接（ESTABL LSHED连接状态，发起端口随机，目标端口固定），-rn查看路由表）
```

##### 网络配置

```
ifconfig：查看和设置网卡信息（eth0第一网卡，eth1第二块网卡，lo回环网卡（虚拟））
ifconfig eth0 192.168.8.250：设置虚拟网卡eth0的IP地址为192.168.8.250

setup：设置IP地址（DHCP[*]自动配置IP地址，没有DHCP服务就去掉*，重启network服务生效（service network restart），永久生效）
```

##### 连接测试

```
ping 192.168.1.1：测试与192.168.1.1的IP地址是否网络相通（它会一直ping，ctrl+c停止）
ping -c 4 192.168.1.1：给192.168.1.1的IP地址发送4个数据包
```

##### 挂载

挂载就是给外接设备（U盘）分配一个盘符

```
mkdir /mnt/cdrom：新建一个cdrom文件夹（一般在mnt里面挂载）
mount /dev/sr0 /mnt/cdrom：将设备sr0挂载到cdrom上（sr0默认挂载设备标识）
umount /dev/sr0：取消挂载设备sr0（前提是不在cdrom挂载文件夹内）
```

### 软件包管理

##### 软件包管理简介

```
源码包（c语言写的包，安装慢，效率高，指定位置安装（一般建议在/user/local/下））
二进制包（RPM包、系统默认包（二进制内容），安装快，默认位置安装）
```

##### 依赖性

```
树形依赖：安装a，需要安装b，需要安装c环形依赖：安装a，需要安装b，需要安装c，需要安装a模块依赖：依赖查询网站www.rpmfind.net解决办法：Linux系统centOS，yum命令安装软件（yum会把依赖的包一并装上）
```

##### 安装、升级、卸载

```
# 没有安装的软件包时，使用包全名，而且要注意路径。如果已经安装软件包是，查询、卸载就不用写全名，使用包名就行。rpm -ivh 包全名：安装软件包（-i安装，-v显示详细信息，-h显示进度，存在依赖性的问题）rpm -Uvh 包全名（-U：升级）# 安装和卸载需要加包全名，其他只需要包名rpm -e 包名（-e：卸载，-q：查询是否安装，-qa：查询所有包，-qi：查询详细信息，-ql：查询包安装位置，-V：查询包文件是否被修改，不用写包全名）# 网络yum源vi /etc/yum.repos.d/CentOS-Base.repo：配置网络yum源（软件池）yum list：查询可用软件包yum search 关键字：查询服务器上和关键字相关的包yum -y install 包名：安装软件包（-y：自动回答yes，不存在依赖性的问题，全自动安装依赖包）yum -y update 包名：升级软件包（-y：自动回答yes，千万要加包名，否则会全部升级，包括内核升级，还会有连接不上等错误）yum -y remove 包名：卸载软件包（-y：自动回答yes，慎用！它会把依赖包也卸载，有可能导致系统错误）yum grouplist：列出所有可用的软件组列表yum grouplist 软件组名：安装指定软件组，组名可以由grouplist查出来（软件组名有空格，则加上引号）yum groupremove 软件组名：卸载指定软件组# 安装源码包# 1.安装C语言编译器（安装gcc）# 2.网站上，下载源码包http://mirror.bit.edu.cn/# 3.复制到Linux系统上# 4.tar -zxvf 包全名：解压安装包，生成软件文件夹# 5.进入软件文件夹（必须要进入cd）# 6../configure --prefix=/usr/local/软件名：软件配置与检查和（prefix）设置安装位置# 7.make：进行编译# 8.make install：编译安装/usr/local/软件名 start：启动该软件服务（指定安装路径启动）rm -rf /usr/local/软件包名：删除该软件包du -sh 文件夹：可以显示文件夹大小# 提醒：同一软件，安装了RPM包，还可以安装源码包，因为安装位置不一样，但启动只能启动一个，因为要占用相同的端口（一般不会装两种包）# 脚本安装包（自动化安装的源码包）# 1.webmin网页图形Linux管理界面# 2.网址：http://sourceforge.net/projects/webadmin/files/webmin/# 3.解压缩，进入压缩目录（tar -zxvf 包全名）# 4.执行安装脚本（Linux一般的执行脚本以.sh结尾，就直接./setup.sh就开始安装了）# 提醒：ctrl+退格键（backspace）删除已输入的字符
```

##### 压缩解压命令

```
zip init.zip init：将init文件压缩为init.zip（保留源文件，-r压缩目录）gzip init：压缩init文件，生成一个init.gz的压缩文件（不保存init文件）gzip Janpan.tar：压缩Janpan.tar就会生成Japan.tar.gz文件（Janpan.tar就不存在了）gunzip init.gz：解压缩文件init.gztar -cvf Japan.tar Japan：将Japan目录打包压缩为Japan.tar(-c打包，v显示详细信息，f指定文件名，保留源文件及目录)tar -zcf Japan.tar.gz Japan：将Japan目录直接压缩打包为Japan.tar.gz（打包同时解压缩）tar -zxf Japan.tar.gz：将Japan.tar.gz解包解压缩（z解压缩，x解包）tar -cjf Japan.tar.bz2 Japan：压缩Japan生成Japan.tar.bz2文件tar -xjf Japan.tar.bz2：解压缩Japan.tar.bz2文件bzip2 -k init：压缩文件init，生成init.bz2（-k保留源文件）unzip init.zip：解压缩文件init.zipbunzip2 init.bz2：解压缩文件init.bz2
```

##### 服务命令

```
# 一般服务放在/etc/rc.d/init.d下/etc/rc.d/init.d/服务名 start：启动该服务（绝对路径启动）service 服务名 status : 查看项目状态service 服务名 start : 启动该项目（源码包安装的服务不能用，因为安装位置不同）service 服务名 restart : 重启该项目service 服务名 stop : 停止该项目
```

### 链接命令

![软硬链接](F:\Project Notebook\Knowledge\Linux系统\Image\软硬链接.png)

##### 硬链接

```
ln /etc/issue /tmp/study.hard：创建文件issue的硬链接study.hard    1. study.hard文件和issue文件，内容、大小、属性都一样    2. study.hard文件能和issue文件同步更新（修改文件任何内容，另一个文件都会更新）    3. 删除源文件，也能正常运行study.hard文件    4. 硬链接类似于拷贝    5. 硬链接文件和源文件i节点一样    6. 不能跨分区    7. 不能对目录使用
```

##### 软链接

```
ln -s /etc/issue /tmp/study.soft：创建文件issue的软链接study.soft    1. study.soft的作用类似于windows的快捷方式，运行study.soft文件就是运行issue文件。    2. study.soft文件的权限是三个rwx，但归根结底使用权限还是issue文件的权限    3. study.soft文件很小，它只是一个符号指向，文件详细信息后面有符号指向。    4. 删除源文件，运行study.soft文件会报错    5. 可以夸分区    6. 可以对目录使用
```

### 时间命令

```
date：获取时间date 031410272014.18：将时间更改为2014年03月14日 10：27：18
```

### 帮助命令

```
man ls：查看ls命令的帮助信息（空格或F向下翻页，回车下翻一行，q退出）man service：查看配置文件service的帮助信息（前面不要加路径）whatis ls：看ls命令的简要的帮助信息ls --help：获取ls命令的选项
```



2、文件相关指令
    文件和文件夹的相关指令，创建、删除、拷贝、移动、查看
    创建：
        文件：  vi 文件路径      touch 文件路径
        文件夹： mkdir 目录路径   创建指定的目录
            mkdir -p dudu/haha/xixi   递归创建目录
    删除
        文件： rm 文件路径     rm -f 文件路径   强制删除
        一般都不删除文件，一般都是备份一下，编辑新的文件
        通配符：*
        rm -f *.txt   删除所有txt文件
        rm -f *       删除所有文件
    

        目录：rmdir 目录路径    只能删除空目录        rm -rf 目录路径    删除非空目录拷贝    cp 源文件路径 目标文件路径        拷贝文件的时候可以修改名字    cp -r 源文件夹 目标文件夹        拷贝文件夹的时候可以修改        cp -r lihong jielun/       使用原来的名字        cp -r lihong jielun/hong   修改名字移动    mv 源文件路径 目标文件路径        移动的时候可以修改文件名字        移动文件夹不用加 -r 参数查看文件    vi就能查看    cat 文件名           -n 显示行号    tac 文件名   倒着查看    head 文件名   默认查看文件前十行        -5  查看文件前五行      tail 文件名   默认查看文件后十行        -5 查看文件后五行    more 文件名        enter ： 往下走一行        空格 ： 往下走一页        不能向上看，按q退出    less 文件名        enter ： 往下走一行        空格 ： 往下走一页        按q退出        pageup   上翻页        pagedown 下翻页        /要查找的字符     也可与查找

4、用户和组
    linux是一个多用户多组的操作系统
    一个用户能否属于多个组  yes
    一个组能否拥有多个用户  yes
    一个用户至少必须属于一个组，一个用户必须拥有自己的主组，其他组称之为附加组
    用户创建
        useradd bajie
        创建成功之后会留下记录，  tail /etc/passwd
        创建一个用户的同时，会给当前用户创建一个名字一模一样的组作为该用户的主组
        给用户添加密码
            passwd 用户名
            这个操作只能在root去给某个普通用户设置密码，在普通用户下只能给自己修改密码，不能设置其他普通用户密码
        -d ： 创建用户的时候指定家目录，不指定会在home下面创建一个和用户名一模一样的目录，一般不指定
        -g : 指定主组，如果不指定，默认创建一个和用户名一模一样的组作为主组
        -G : 指定附加组
        -u ：指定用户id    一般都不用
    用户修改
        usermod
        -g : 修改主组
            usermod -g 501 bajie   修改bajie主组
        -l : 修改用户名
            usermod -l wuneng bajie   将bajie用户名修改为wuneng
        -u : 修改用户id
            usermod -u 505 wuneng   将wuneng用户id修改为505
        -d : 修改家目录
            usermod -d /home/lala wuneng   不用
    用户删除
        userdel
            userdel 用户名     只删除文件中的记录
            userdel -r 用户名  将家目录一并删除
            如果操作不规范，家目录也可手动干掉
    用户切换
        centos里面
        su 用户名
        从root切换到普通不用密码
        从普通切换到root，需要输入root的密码，通过exit返回上一个用户
        这里面不能sudo，因为不支持，如果要支持，需要相关配置
    

        Ubuntu里面    不允许root直接登录，需要配置才可以。    用普通用户登录。  sudo 指令，提示输入密码，这个密码是当前用户的密码组创建    查看当前组，  tail /etc/group    groupadd 组名    -g : 可以指定组id删除组    groupdel 组名    【注】如果一个组是主组的话，这个组删不掉    【注】如果一个组是一个用户的主组，并且仅仅是这个用户的主组，而且组名和用户名相同，那么在删除用户的同时，该组也就删除了修改组    groupmod    -g : 修改组的id号    groupmod -g 513 dudu    -n : 修改组名        groupmod -n xixi dudu

5、文件权限
    权限什么意思？系统中，文件的权限都有哪些？读、写、执行
    读：read   r   写：write   w    执行：execute  x
    如果写一个-代表没有这个权限
    权限表示
    rwx     111     7   
    rw-     110     6
    r-x     101     5
    r--     100     4
    -wx     011     3
    -w-     010     2
    --x     001     1
    ---     000     0
    

    rwx             r-x             r-x所属用户权限     组内用户权限     组外用户权限权限表示法：0755   0777   0644修改权限修改组的指令不是乱用的，需要root用户的权限才能修改，Ubuntu下需要使用sudo，centos需要切换root执行修改权限：chmod    格式  chmod 权限 文件路径    chmod 755 1.txt    chmod g+w,g-x 1.txt        u : 修改所属用户        g : 修改组内用户        o : 修改组外用户    目录权限修改        chmod 777 目录路径    只修改该目录的权限        chmod -R 777 目录路径   递归修改目录里面所有文件的权限修改用户：chown    chown 用户名 文件路径         只修改用户名    chown 用户名:组名 文件路径     用户和组都修改    chown :组名 文件路径          只修改组名    chown -R 用户名:组名 目录路径             递归修改目录里面所有文件的用户和组修改组：chgrp    chgrp 组名 文件路径    chgrp -R 组名 目录路径      递归修改umask    是什么？    系统创建文件默认权限是  644    系统创建目录默认权限是  755    目录默认比文件多了一个可执行权限，对目录来说，可执行就是打开目录    umask就决定了文件和目录的默认权限        0777-0022 = 0755  这就是默认权限，文件都少可执行权限    指定umask进行修改，将umask指定为0011        0777-0011 = 0766(目录)  0666（文件）

6、文件搜索
    find
    用法如下：
    find   在哪找   怎么找   找什么
    在哪找：就是一个路径，默认是当前路径
    怎么找：按照名字、大小、用户，其实就是参数
        -name : 按照名字找
        -size : 按照大小找
        -user : 按照用户找
        -group : 按照组找
        -maxdepth : 查找最大目录级别
        -mindepth : 查找最小目录级别
    找什么：1.mp3  *.txt
    

    find / -name dudu.pyfind / -size 10k     等于10k的文件             +10k     大于10k的文件            -10k     小于10k的文件find / *.txt -user liuyanfind / -maxdepth 3 -mindepth 2 -name *.txt  找指定级别的文件

day09-linux

1、文件内容搜索
    grep 内容 文件路径
    参数：
    -i ：忽略大小写
    --color=auto : 颜色自动提示，将grep设置为默认颜色提示，其实就是可以给grep指令器别名
        vi ~/.bashrc
        添加一句  alias grep='grep --color=auto'
        source ~/.bashrc
    -n : 显示内容出现的行号
    -l : 显示内容出现的文件名
    -c : 显示出现该内容的次数
    

    也可以写正则表达式, 注意使用 -P    13838384380    \d{11}    ^1\d{10}    3456789    ^1[3-9]\d{9}    test@qq.com   duduxixi@163.com  lalahehe@sina.cn    \w+@\w+\.(com|cn|net)grep 王者荣耀 1.txtgrep 王者荣耀 *.txtgrep 王者荣耀 ~/.txtgrep -P '1[3-9]\d{9}' 3.txt 

2、管道
    格式： 指令1 | 指令2
    指令1的输出作为指令2的输入，指令2的输出显示到屏幕中
    常用的管道指令有：
        ls -l /etc | less
        ls -l /etc | head -5
        ls -l /etc | tail -5
        ls -l /etc | head -10 | tail -5
        ls -l /etc | grep 找的内容
    查看进程相关
        ps -ef | grep ssh
3、搭建主机信任
    密码学的内容，加密-解密，用到一个东西  秘钥
    加密-解密秘钥相同-对称加解密
    加密-解密秘钥不相同-非对称加解密
    一对儿秘钥：公钥和私钥
    公钥：给你们，你们拿的都是公钥
    私钥：我自己拥有，
    公钥加密-私钥解密，私钥加密-公钥解密
    实现免密码登录，linux1登录linux2，实现免密码登录
    （1）在linux1上，生成公钥和私钥
        ssh-keygen   一路敲enter即可
    （2）来到生成秘钥的文件中
        id_rsa : 私钥
        id_rsa.pub : 公钥
    （3）复制公钥
    （4）来到linux2中
        vi ~/.ssh/authorized_keys
        将公钥粘贴进来即可
    这样在通过linux1登录linux2的时候就实现了免密码登录
6、scp
    scp：基于ssh的cp，cp是实现本机之间来回拷贝，scp在两台linux之间进行拷贝
    scp的用法：
        scp 源路径 目标路径
        scp 1.txt root@ip地址:路径
        如果发送文件夹，需要添加 -r 选项
    linux和linux之间使用scp进行互发，如果搭建了主机信任，不用输入密码
    winscp，实现windows和linux之间使用scp进行互发
        安装，使用即可，左边：windows目录，右边：linux目录，相互拖动即可
4、重定向
    标准输入（stdin, 键盘）、标准输出（stdout, 屏幕）
    输出重定向：意思就是不输出到屏幕，输出到其他地方
    ls -l > 1.txt      >作用：首先清空文件，然后写入文件
    ls -l >> 1.txt     >>作用：追加内容
    

    错误重定向：指令有错，错误信息显示到哪里ls /lala 2> 1.txt   将错误信息显示到指定文件中ls /lala 2>> 1.txt  将错误信息追加到指定文件中

5、挂载、磁盘相关指令
    挂载：神马意思？看图形
    将u盘和目录对应的过程就是挂载
    （1）插上u盘
        u盘只能让你的linux识别，如果是虚拟机，在虚拟机设置里面点击让虚拟机识别，
    （2）linux识别成功之后，通过指令查看你的设备
        fdisk -l
        /dev/sda   就是linux系统的硬盘设备
        如果有分区  /dev/sda1   /dev/sda2  xxx
    

        u盘设备往下走    /dev/sdb   就是你的u盘设备    如果有分区  /dev/sdb1   /dev/sdb2    挂载u盘    mount -t  需要挂载的设备  挂载点        auto : 自动识别        vfat : fat32        ntfs-3g : ntfs格式   需要插件支持    -o iocharset=utf8  如果有中文，可以指定字符集    mount /dev/sdb1 /mnt/usb    取消挂载，不能再挂载的目录中取消挂载    umount /dev/sdb1 /mnt/usb    umount /dev/sdb1    umount /mnt/usb    如果取消挂载时候显示该设备正在忙，需要输入指令把使用的进程给干掉，再取消挂载即可    fuser -m -k /mnt/usb和磁盘相关的指令df    显示当前可用的设备的使用情况    -h  人性化的显示大小du    当前目录的使用情况    -h  人性化的方式显示大小配置开机挂载vi /etc/fstab添加一行信息/dev/sdb1     /mnt/usb      vfat    defaults      0 0

7、软硬链接
    link，为了解决文件的共享问题，引入了链接机制。分为软链接和硬链接，以软链接使用居多
    硬链接
        ln 源文件 目标文件
        也可以使用link
        链接之后，目标文件和源文件内容相同，修改其中一个，另外一个也被修改
        在ll之后，可以看见硬链接个数，增加
        删除其中一个，另外一个不受影响
        可以理解为，给一个文件起了一个外号、别名  
        【注1】不能给目录创建
        【注2】创建完硬链接之后，你的用户名和组信息不变
    软链接
        ln -s 源文件 目标文件
        软链接创建之后，修改其中一个，另一个也修改
        【注1】可以给目录创建
        【注2】创建完之后，用户和组信息是创建时候的信息
    软硬链接的不同之处
        在linux里面，存放一个文件，由三部分组成，一个文件名，一个是文件索引（inode），一个是数据部分
        见百鸟朝凤图
8、压缩和解压（很常用）
    在linux里面，常见压缩格式有两种，一种叫做gz，一种叫做bz2
    gzip\gunzip(后缀名是.gz)
        gzip 文件1 文件2
        生成之后，源文件不在了，只有压缩文件，每一个都生成一个压缩文件
        gunzip 文件
        不能实现打包压缩，不能实现保留源文件
    bzip2\bunzip2(后缀名是.bz2)
        bzip2 文件1 文件2
        每一个生成一个压缩文件
        -k : 保留源文件
        bunzip2 压缩文件1 压缩文件2
    tar（可以实现压缩和解压，可以实现打包的功能）
        如果打包压缩使用的gzip压缩的，那么后缀名  .tar.gz    .tgz
        如果打包压缩使用的bzip2压缩的，那么后缀名  .tar.bz2   
        常用的参数有：
        -z : 使用gzip压缩
        -j : 使用bzip2压缩
        -f : 打包压缩的时候指定压缩后的文件名
        -c : 打包文件
        -x : 解压缩使用的
        -v : 压缩和解压缩时候显示进度
    

    打包使用gzip压缩：    tar -zcvf 压缩后的名字.tar.gz 文件1 文件2 文件3使用gzip解压缩    tar -zxvf 压缩包.tar.gz打包使用bzip2压缩    tar -jcvf 压缩后的名字.tar.bz2 文件1 文件2 文件3使用bzip2解压缩    tar -jxvf 压缩包.tar.bz2

9、软件安装之yum安装
    红帽系列软件安装使用  yum安装
    大便系列软件安装使用  apt-get安装
    去哪下载软件呢？yum源，这个源在哪呢？默认都有自己的源，但是这个源是在国外的。所以使用linux经常将源设置为国内源，阿里源、清华源、搜狐源、网易源、中科大源
    如何配置为国内源？
    打开阿里源，点击帮助
    （1）mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
    （2）下载对应的源配置文件
    wget是一个专业的下载软件，但是需要安装
    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
    或者
    curl是自带的，不用安装
    curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
    （3）执行
        如果是本地，需要网络，吃饭的时候执行，晚上执行，热点执行
        yum clean all
        yum make cache


day10-linux

1、软件安装
    （1）yum安装（多）
        yum install -y 包名   中间一路yes
        yum remove -y 包名
        可以只下载安装包，不安装
        yum install -y --downloadonly --downloaddir=./ wget
        下载就是.rpm的包。
    （2）rpm安装
        不论你用的是yum还是用的rpm安装，其实安装的都是rpm包。在linux里面，安装软件的时候，不仅仅是安装这么一个软件，与之对应的要按照很多的依赖软件
        a ==》 b===》c==》d
        如果使用rpm安装，你要知道软件依赖关系才能安装，但是使用yum的话，不用知道依赖关系，yum自动为你解决
        比如  yum install -y --downloadonly --downloaddir=./ vim
            包含vim的包以及vim依赖的包，全部下载下来之后，估计10个包，这10个都是rpm，请问先装哪个后装哪个。
            yum install -y vim   依赖关系自动解决
        -ivh ：安装     rpm -ivh 包.rpm
        -e ：卸载       rpm -e wget
        -ql : 列出包安装路径   rpm -ql wget
        -qi : 列出指定包的详细信息  rpm -qi wget
    （3）编译安装（多）
        相对来说，编译安装是需要编译源码的，安装的软件更加适合你的电脑，你的软硬件环境，更加的稳定，相比较yum来说稳定
        编译安装3个步骤：
        （1）配置
            ./configure --prefix=你安装路径 --以及其它参数
        （2）编译
            linux里面的软件都是使用c、c++写的，所以你得有编译器
            gcc gcc-c++
            yum install -y gcc gcc-c++
            make 
        （3）安装
            make install
        走完一步之后，可以执行一个指令  echo $?  ,如果返回0，代表上面指令执行成功，如果返回其它，说明执行失败
        指令可以连写：   make && make install
        安装ntfs-3g
        安装python
2、服务和进程相关指令
    linux的启动等级，打开这个文件   vi /etc/inittab
    0 : 关机等级
    1 : 单用户模式
    2 : 多用户的无网络模式
    3 : 多用户模式，有网络
    4 : 保留模式
    5 : 界面模式
    6 : 重启模式
    

    切换等级   init 0   init 1   init 6
    查看当前等级  runlevel   who -r
    whoami  : 我是谁，查看当前用户
    
    查看随开机启动的服务
    chkconfig --list
    赵灵儿
    随开机启动的服务，我们给他们起了一个非常好听的名字，守护进程（daemon）
    sshd   httpd   mysqld  其实就是一个随机开机启动的服务
    
    开启、关闭服务
        要有控制开启、关闭服务的脚本，比如iptables（防火墙）
        /etc/init.d/iptables start | stop | restart
        /etc/init.d/network start | stop | restart
        经常找脚本，太不方便了，将服务脚本放到  /etc/init.d ,如果支持服务模式，那么就可以使用如下指令开启和关闭
        service iptables start | stop | restart
        service network start | stop | restart
    
        一般情况，安装服务的时候，控制服务的脚本在安装包就有，但是有的没有，比如nginx没有
        自己按照的服务，你就可以将脚本放到  /etc/init.d 里面，然后通过service控制它的开启和关闭  service nginx start
    
    自己按照的服务随开机启动
        chkconfig nginx on   默认设置的等级为2345
        chkconfig nginx off
        还得给脚本权限，权限一般设置为755
        通过chkconfig --list 查看有没有配置成功
    
    进程相关指令
        top ： 实时查看系统的运行情况
        w ：查看系统的当前用户的链接情况
        free : -h  内存的使用情况
        ps : 查看进程相关信息
            ps -ef | grep ssh
            ps aux | grep ssh
        kill : 杀死一个进程
            kill -9 进程id
        netstat -lnp : 查看网络和端口使用情况
            netstat -lnp | grep 80

3、shell简介(了解一下)
    shell编程   wget url    包.tar.gz
    python break : 终止循环
           continue : 结束当次循环，进入下一次循环
4、ftp服务搭建
    ftp是什么？文件传输协议，用在将本地文件上传到服务器
5、nfs搭建
    nfs是什么？可以实现linux之间的文件共享
    nfs客户端还有服务端
6、nginx服务搭建
    nginx是什么? web服务器   apache打交道
    nginx服务器的根目录（www）在   /usr/local/nginx/html
    ip:端口     域名（jd.com   baidu.com   taobao.com   mi.com）  sb.com
    DNS服务商，阿里云、腾讯云都有
    

    一个服务器是否能放多个网站呢？可以的，配置虚拟主机

7、各系统指令区别总结
    centos6.8
    centos7.0
    ubuntu16.04

需要执行的下载指令有
yum install -y gcc gcc-c++
yum install -y zlib*
yum install -y nfs-utils
yum install -y gcc openssl-devel perl
yum install -y gcc gcc-c++ autoconf automake zlib zlib-devel openssl openssl-devel pcre pcre-devel


# Linux命令

linux文件路径是以/（根）开头的树杈状文件系统

### 包管理

```
# 安装安装包
yum install (包名) 
```

```
# 卸载软件
yum remove (包名)
```

### 文件管理

删除文件

```
rm -f name	强行删除当前文件夹下名为name的文件
```

删除文件

```
rm -rf name/  强行删除当前文件夹下名为name的文件夹，包括name文件夹里的所有内容
```

### 服务管理

启动服务（以docker服务为例）

```
systemctl start docker.service
```

关闭服务

```
systemctl stop docker.service
```

重启服务

```
systemctl restart docker.service
```

显示服务状态

```
systemctl status docker.service
```

设置服务自启动

```
systemctl enable docker.service
```

禁止服务自启动

```
systemctl disable docker.service
```

查看服务是否自启动

```
systemctl is-enabled docker.service
```

列出所有自启动服务

```
systemctl list-unit-files|grep enabled
```

列出系统所有服务的启动情况

```
systemctl list-units --type=service
```

### 进程管理

查看进程

```
ps -A 						显示所有进程
```

结束进程

```
killall -9 mysql 			结束名称为mysql的进程（包括同名进程） 
```

### 内容修改

打开文件

```
vim my.cnf					在当前文件夹下打开名称为my.cnf文件
```

修改内容

```
按“i”键，进入编辑模式，开始编辑。
按“esc”键，退出编辑模式，结束编辑。
```

是否保存

注意：要退出编辑模式

```
:（冒号不要掉）wq				保存编辑
:q!							 不保存编辑
```

**说明**：本文中对Linux命令的讲解都是基于名为CentOS的Linux发行版本，我自己使用的是阿里云服务器，系统版本为CentOS Linux release 7.6.1810。不同的Linux发行版本在Shell命令和工具程序上会有一些差别，但是这些差别是很小的。
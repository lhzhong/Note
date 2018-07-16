## 一般模式下移动光标
| 快捷键                       | 作用              |
| :--------------------------:|--------------------|
| **h/左方向键**               | 光标向左移动一个字符 |
| **j/下方向键**               | 光标向下移动一个字符 |
| **K/上方向键**               | 光标向上移动一个字符 |
| **l/右方向键**               | 光标向右移动一个字符 |
| **Ctrl+f/pageup**           | 屏幕向前移动一页 |
| **Ctrl+b/pagedown**         | 屏幕向后移动一页 |
| Ctrl+d                      | 屏幕向前移动半页 |
| Ctrl+u                      | 屏幕向后移动半页 |
| +                           | 光标移动到非空格符的下一列 |
| -                           | 光标移动到非空格符的上一列 |
| n+空格                      | 按下数字n然后按空格，则光标向右移动n个字符，如果该行字符数小于n，则光标继续从下行开始向右移动，一直到n |
| **0/Shift+6**               | 移动到本行行首 |
| **Shift+4**                 | 即’$’移动到本行行尾 |
| H                           | 光标移动到当前屏幕的最顶行 |
| M                           | 光标移动到当前屏幕的中央那一行 |
| L                           | 光标移动到当前屏幕的最底行 |
| **G**                       | 光标移动到文本的最末行 |
| **n+G**                     | 移动到该文本的第n行 |
| gg                          | 移动带该文本的首行|
| n+回车                      | 光标向下移动n行 |

## 一般模式下查找与替换
| 快捷键                        | 作用                             |
| :---------------------------:|----------------------------------|
| **/word**                    | 向光标之后寻找一个字符串名为word的字符串，当找到第一个word后，按”n”继续搜后一个 |
| **?word**                    | 想光标之前寻找一个字符串名为word的字符串，当找到第一个word后，按”n”继续搜前一个 |
| **:n1,n2s/word1/word2/g**    | 在n1和n2行间查找word1这个字符串并替换为word2，你也可以把”/”换成”#” |
| **:1,$s/word1/word2/g**      | 从第一行到最末行，查找word1并替换成word2 |
| :1,$s/word1/word2/gc         | 加上c的作用是，在替换前需要用户确认 |

## 一般模式下删除、复制粘贴
| 快捷键                        | 作用                             |
| :---------------------------:|----------------------------------|
| **x,X**                      | x为向后删除一个字符，X为向前删除一个字符 |
| nx                           | 向后删除n个字符 |
| **dd**                       | 删除光标所在的那一行 |
| **ndd**                      | 删除光标所在的向下n行 |
| d1G                          | 删除光标所在行到第一行的所有数据 |
| dG                           | 删除光标所在行到末行的所有数据 |
| **yy**                       | 复制光标所在的那行|
| **nyy**                      | 复制从光标所在行起向下n行 |
| **p,P**                      | p复制的数据从光标下一行粘贴，P则从光标上一行粘贴 |
| y1G                          | 复制光标所在行到第一行的所有数据 |
| yG                           | 复制光标所在行到末行的所有数据 |
| J                            | 将光标所在行与下一行的数据结合成同一行 |
| **u**                        | 还原过去的操作 |

## 进入编辑模式
| 快捷键                        | 作用                             |
| :---------------------------:|----------------------------------|
| **i**                        | 在当前字符前插入字符 |
| **I**                        | 在当前行行首插入字符 |
| **a**                        | 在当前字符后插入字符” |
| **A**                        | 在当前行行末插入字符 |
| **o**                        | 在当前行下插入新的一行 |
| **O**                        | 在当前行上插入新的一行 |
| r                            | 替换光标所在的字符，只替换一次 |
| R                            | 一直替换光标所在的字符，一直到按下ESC |

## 命令模式
| 快捷键                        | 作用                             |
| :---------------------------:|----------------------------------|
| **:w**                       | 将编辑过的文本保存 |
| **:w!**                      | 若文本属性为只读时，强制保存 |
| **:q**                       | 退出vim |
| **:q!**                      | 不管编辑或未编辑都不保存退出 |
| **:wq**                      | 保存，退出 |
| :e!                          | 将文档还原成最原始状态 |
| ZZ                           | 若文档没有改动，则不储存离开，若文档改动过，则储存后离开，等同于:wq |
| :w [filename]                | 编辑后的文档另存为filename |
| :r [filename]                | 在当前光标所在行的下面读入filename文档的内容 |
| **:set nu**                  | 在每行的行首显示行号 |
| **:set nonu**                | 取消行号 |
| n1,n2 w [filename]           | 将n1到n2的内容另存为filename这个文档 |
| :! command                   | 暂时离开vim运行某个linux命令，例如 :! ls /home 暂时列出/home目录下的文件，然后会提示按回车回到vim |

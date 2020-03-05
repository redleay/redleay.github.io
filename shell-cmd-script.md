# Linux Shell命令与脚本

## Shell脚本执行选项
| 示例           | 功能                                 |
| ------------   | ------------                         |
| sh -n run.sh   | 只读取shell脚本，但不实际执行        |
| sh -x run.sh   | 进入跟踪方式，显示所执行的每一条命令 |
| sh -c "string" | 从strings中读取命令                  |

## 字符串替换
| 示例                             | 功能                                                                          |
| ------------                     | ------------                                                                  |
| ${#string}                       | 获取$string的长度                                                             |
| ${string:position}               | 在$string中, 从位置$position开始提取子串                                      |
| ${string:position:length}        | 在$string中, 从位置$position开始提取长度为$length的子串                       |
| ${string#substring}              | 从变量$string的开头, 删除最短匹配$substring的子串                             |
| ${string##substring}             | 从变量$string的开头, 删除最长匹配$substring的子串                             |
| ${string%substring}              | 从变量$string的结尾, 删除最短匹配$substring的子串                             |
| ${string%%substring}             | 从变量$string的结尾, 删除最长匹配$substring的子串                             |
| ${string/substring/replacement}  | 使用$replacement, 来代替第一个匹配的$substring                                |
| ${string//substring/replacement} | 使用$replacement, 代替所有匹配的$substring                                    |
| ${string/#substring/replacement} | 如果$string的前缀匹配$substring, 那么就用$replacement来代替匹配到的$substring |
| ${string/%substring/replacement} | 如果$string的后缀匹配$substring, 那么就用$replacement来代替匹配到的$substring |

## sed
| 示例                           | 功能                                          |
| ------------                   | ------------                                  |
| sed -i '3s/aaa/fff/' file      | 对file中的第3行，将其中的aaa替换为fff         |
| sed -i 's/^/fff/' file         | 对file中的所有行，在行首插入fff               |
| sed -i '/xxx/s/aaa/fff/g' file | 对file找出包含xxx的行，并将其中的aaa替换为fff |
| sed -i '1s/[#\*]/fff/gp' file  | 对file第1行，将其中的#号或是\*号替换为fff     |

## sort
| 示例                                | 功能                                                                          |
| ------------                        | ------------                                                                  |
| sort -n                             | 以数值来排序                                                                  |
| sort -t \_ -k 2 -n                  | 以"\_"为分隔符，以第2列进行数值排序                                           |
| sort -t \_ -k2n -k3n -s             | 以"\_"为分隔符，先第2列进行数值排序，后第3列进行稳定的数值排序                |
| sort -t \_ -k2n | sort -t . -k1n -s | 先以"\_"为分隔符，第2列进行数值排序，后以"."为分隔符，第1列进行稳定的数值排序 |

## gdb调试
| 示例                                    | 功能                                                   |
| ------------                            | ------------                                           |
| show dir                                | 查看当前gdb搜索源码的路径                              |
| dir dirname                             | 添加新的源码路径到搜索路径，多个时用冒号分开           |
| display                                 | 自动打印调试信息                                       |
| undisplay                               | 取消自动打印调试信息                                   |
| tb                                      | 临时断点                                               |
| attach PID                              | 附上PID进程并进入调试                                  |
| set substitute-path from\_path to\_path | 映射源码搜索路径中的部分string为其他string             |
| set scheduler-locking off               | 执行所有thread                                         |
| set scheduler-locking on                | 只执行当前thread                                       |
| set scheduler-locking step              | 单步时，除了next过一个函数的情况以外，只执行当前thread |

## 压缩
| 示例                                      | 功能                                 |
| ------------                              | ------------                         |
| tar -c[zj]vf archive.tar.gz bin/ lib/     | 创建归档，将bin和lib目录归档到压缩包 |
| tar -x[zj]vf archive.tar.gz -C DIR        | 解压归档，将压缩包解压到DIR目录      |
| tar -t[zj]vf archive.tar.gz               | 查看归档，查看压缩包内文件列表       |
| zip archive.zip -r ffmpeg/ pooltrans-1.0/ | 创建归档                             |

## ln链接
| 示例                | 功能                     |
| ------------        | ------------             |
| ln -s file softlink | 为file创建软链接softlink |
| ln file hardlink    | 为file创建硬链接hardlink |

## 前后台调度
| 示例         | 功能                                                        |
| ------------ | ------------                                                |
| jobs         | 查看正在运行的任务状态                                      |
| fg jobnumber | 将任务调度到前台运行，不带jobnumber时表示对最后一个进程操作 |
| bg jobnumber | 将任务调度到后台运行，不带jobnumber时表示对最后一个进程操作 |
| Ctrl-Z       | 将前台任务调度到后台中暂停，显示jobnumber                   |

## 环境
| 示例                                                    | 功能               |
| ------------                                            | ------------       |
| export LD\_LIBRARY\_PATH=$LD\_LIBRARY_PATH:/path/to/lib | 设置动态库搜索路径 |
| strings /lib64/libc.so.6 \| grep GLIBC                  | 查看库文件中的string |

## 编译
| 示例                | 功能               |
| ------------        | ------------       |
| make VERBOSE=1      | 打印make执行的命令 |
| readelf -S exe\|lib | 查询exe或lib是否存在\_debug开头的段，有则携带debug信息 |

## 语法
| 示例                                    | 功能                           |
| ------------                            | ------------                   |
| for i in {1..100}; do echo $i; done     | 循环                           |
| for i in $(seq $m $n); do echo $i; done | 循环，循环起止由变量$m和$n控制 |
| for f in `ls . | tr " " "\?"`; do echo $i; done | 循环文件名带空格的目录 |


## 其他常用命令
```
pip install opencv-python -i http://mirror-sng.oa.com/pypi/web/simple/ --trusted-host mirror-sng.oa.com
```

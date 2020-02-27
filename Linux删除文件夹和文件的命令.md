## Linux删除文件夹和文件的命令

Linux删除目录很简单，使用rm -rf命令即可。
使用规则：

    rm -rf 目录名字   
    
    -r 向下递归，不管有多少级目录，一并删除
    -f 直接强行删除，没有任何提示
示例：
    删除文件夹实例：
    rm -rf /var/log/httpd
    将会删除/var/log/httpd目录以及其下所有文件、文件夹

    删除文件使用实例：
    rm -f /var/log/httpd/access.log
    将会强制删除/var/log/httpd/access.log这个文件

注意：使用 rm -rf 的时候一定要小心，Linux没有回收站。


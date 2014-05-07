#shell命令使用记载

**在所有jar中查找包含biz-ao.xml的jar，并把这个jar文件名输出：**
```shell
 find . -type f -name "*.jar" |while read line ;do   unzip -l  $line |grep "biz-ao.xml"; if [ $? -eq 0 ] ; then echo $line ; fi ; done
```
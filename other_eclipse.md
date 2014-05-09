#eclipse工程下的.project文件和.classpath文件认识
大家都知道一组java文件目录是否是一个eclipse工程,且是否能够导入到eclipse所识别,主要取决是否有.project和.classpath文件.
#### .project文件
```xml
<projectDescription>
  <name>工程名称 </name>
  <comment>工程说明</comment>
  <projects>
    <project>所依赖的工程1 </project>
    <project>所依赖的工程2</project>
  </projects>
  <buildSpec>
    <buildCommand>
      <name>org.eclipse.jdt.core.javabuilder</name>
    </buildCommand>
  </buildSpec>
  <natures>
    <nature>org.eclipse.jdt.core.javanature</nature>
  </natures>
</projectDescription>
```

####.classpath文件
主要是对工程所使用到关于类相关路径环境的描述.  
.Classpath文件的结构很简单.只有classpath元素下包含着多个Classpathentry有以下几个属性:
Kind: 代表设置的path种类.种类有:
   src:描述path路径为源代码的路径,eg:
```xml
<classpathentry kind="src" path="src/test/java" output="target/jboss/test-classes" including="**/*.java" excluding="**/.svn/"/>
```
output:源文件编译以后的输出的文件路径.java则是class 文件.eg:  
```xml
<classpathentry kind="output" path="target/jboss/classes"/>
```
lib:工程所用到的library的路径信息
var: 也代表工程所使用到的库文件或者目录.只是kind = "var"标示这这个路径带有全局编译路径中设置的
变量(Window->Prefrences->Java->Build Path->Classpath Variables),例如下面的“M2_REPO”就是代表的maven仓库的环境变量路径。eg:
```xml
<classpathentry kind="var" path="M2_REPO/javax/activation/activation/1.1/activation-1.1.jar" sourcepath="M2_REPO/javax/activation/activation/1.1/activation-1.1-sources.jar"/>
```
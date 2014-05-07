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

####classpath文件
Classpath文件的结构很简单.只有classpath元素下包含着多个
Classpathentry有以下几个属性:
Kind: 代表设置的path种类.种类有:
Src:代表path代码的路径为源文件,output:源文件编译以后的编译文件是什么.java则是class 文件.
Var 
Output:
Lib:
eg1:  
```xml
<classpathentry kind="src" path="src/test/java" output="target/jboss/test-classes" including="**/*.java" excluding="**/.svn/"/>
```

Eg2:  
```xml
<classpathentry kind="output" path="target/jboss/classes"/>
```
Eg3:  
```xml
<classpathentry kind="var" path="M2_REPO/javax/activation/activation/1.1/activation-1.1.jar" sourcepath="M2_REPO/javax/activation/activation/1.1/activation-1.1-sources.jar"/>
```
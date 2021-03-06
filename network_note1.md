#网络通信、传输的理解和体会随记  

###前记
&emsp;&emsp;&emsp;&emsp;这段时间一直在开发一个关于游戏消息分发的中间件，在这个过程中涉及到数据传输在网络传输过程中碰到的编码问题,以下是我在解决这些问题过程中一些自我体会和理解。
####数据在网络中的传输方式  
&emsp;&emsp;&emsp;&emsp;数据(文本,图片,语音等)在网络中传输本质都是以二进制流(byte流)传输的，但是在传输的过程中需要按照不同的数据格式进行编码&解码---如果是向外发送消息，则需要按照指定的数据格式编码(即把数据按照一定的格式拆解成二进制数组)，在接受消息时需要按照指定的数据格式解码成数据(即把传输过来的二进制流按照其解码的格式组装成应用程序可以识别的数据)，例如:  
- 传输字符时按照使用的字符集(GBK,UTF-8等)的不同,所编码出的二进制流也不一样  
- 传输jpg，gif，protobuf都有自己的编码格式  
**所以在网络通信中,我们可以得出两个结论:**  
- 客户端根据不同的内容按照自己的格式编码成二进制流传输到服务端后，服务端必须要知道这个二进制流的编码类型，才可以按照格式类型解码.  
- 因为不管传输什么类型的数据最后都是编码成二进制流进行传输，所以在一次网络传输过程中我们的二进制流可以是文字，图片，声音等不同类型数据的组合。  

####什么是协议
&emsp;&emsp;&emsp;&emsp;**协议是对数据在网络传输过程中语义层的描述。**这个语义可能包括着对传输过程中字节流的含义，也可能包含着业务层面上的含义,例如:  
- 场景1:由于其网络传输的本质都是二进制流，所以客户端向服务端传输的二进制流中，可能由不同段的二进制流组成，例如：客户端既要向服务端传输一段文本，同时又要传输一张图片，这个时候这两段不同的类型的数据按照各自的编码格式编码成一段二进制流，然后打包整体发送给服务端，这个时候服务端必须知道这段二进制里面从哪一段到哪一段是文本字符的二进制流，其编码类型是什么样的？哪一段又是图片的二进制流，其实编码类型又是什么样的？这样服务端才可以把这段二进制解码还原。这里面对编码类型，以及不同类型二进制流之间区分的描述，就是协议需要做的事情  
- 场景2:假设客户端向服务端发送一个登陆请求消息，这个消息传输的是一段文本字节流其中包含在用户登陆的请求在服务端的请求路径、用户名和密码，那么服务端在接受到这个消息后，除了本身要按照客户端编码的字符集进行解码获得应用程序可以读取的文本数据以外，还需要按照业务意义解析出这段文本字符中哪一段长度是代表的请求路径，哪一段长度代表的是用户名和密码。
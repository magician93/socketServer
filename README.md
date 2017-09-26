# create a tcp server on android
应用场景：物联网，上位机与下位机通讯

日后准备添加的功能：
1、tcpclient
2、websocket server 
3、websocket client
4、串口 read write
5、串口转tcp server
6、串口映射
7、串口跨内网映射

install: 

``````
cordova plugin add https://github.com/huge818/socketServer.git
````````

example
```````````
document.addEventListener("deviceready", function(){
	var socketServer=cordova.plugins.socketServer;
	socketServer.startServer(8080,function(data){
		if(data.type=="data"){
			var socketId=data.socketId;
			console.log("length: "+data.length);
			console.log("socketId: "+data.socketId);
			console.log("HostAddress: "+data.HostAddress);
			console.log("HostName: "+data.HostName);
			socketServer.write(socketId,"server reply: ok:"+ data.buffer); //base64
		}
		else if(data.type=="connect"){
			console.log("connect");
			console.log("socketId: "+data.socketId);
		}
		else if(data.type=="close"){
			console.log("close");
			console.log("socketId: "+data.socketId);
		}
	  	var str=JSON.stringify(data);
	  	console.log(str);
	},function(){
		console.log("error");
	});

}, false);

```````````




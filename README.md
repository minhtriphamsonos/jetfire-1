jetfire
=======

WebSocket [RFC 6455](http://tools.ietf.org/html/rfc6455) client library for iOS and OSX.

Jetfire conforms to all of the base [Autobahn test suite](http://autobahn.ws/testsuite/). The library is very simple and only a few hundred lines of code, but fully featured. It runs completely on a background thread, so processing will never block the main thread. 

jetfire also has a Swift counter part here: [starscream](https://github.com/daltoniam/starscream)

## Example ##

Open a connection to your websocket server. self.socket is a property, so it can stick around.

```objc
self.socket = [[JFWebSocket alloc] initWithURL:[NSURL URLWithString:@"ws://localhost:8080"]];
self.socket.delegate = self;
[self.socket connect];
```

Now for the delegate methods.

```objc
/////////////////////////////////////////////////////////////////////////////
-(void)websocketDidConnect:(JFWebSocket*)socket
{
    NSLog(@"websocket is connected");
}
/////////////////////////////////////////////////////////////////////////////
-(void)websocketDidDisconnect:(JFWebSocket*)socket error:(NSError*)error
{
    NSLog(@"websocket is disconnected: %@",[error localizedDescription]);
}
/////////////////////////////////////////////////////////////////////////////
-(void)websocket:(JFWebSocket*)socket didReceiveMessage:(NSString*)string
{
    NSLog(@"got some text: %@",string);
    dispatch_async(dispatch_get_main_queue(),^{
	//do some UI work
    });
}
/////////////////////////////////////////////////////////////////////////////
-(void)websocket:(JFWebSocket*)socket didReceiveData:(NSData*)data
{
    NSLog(@"got some binary data: %d",data.length);
}
```

How to send a message.

```objc
-(void)sendMessage
{
	[self.socket writeString:@"hello server!"];
	//[self.socket writeData:[NSData data]]; you can also write binary data like so
}
```

Disconnect.

```objc
-(void)disconnect
{
	[self.socket disconnect];
}
```


## Install ##

The recommended approach for installing jetfire is via the CocoaPods package manager (like most libraries). 

## Requirements ##

jetfire requires at least iOS 5/OSX 10.7 or above.


## License ##

jetfire is license under the Apache License.

## Contact ##

### Austin Cherry ###
* https://github.com/acmacalister
* http://twitter.com/acmacalister
* http://austincherry.me

### Dalton Cherry ###
* https://github.com/daltoniam
* http://twitter.com/daltoniam
* http://daltoniam.com
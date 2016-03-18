# CDN---IOS-SERVER-SELECTOR-



<b>What is this?</b>

Eg. if you use <b>CDNsun</b> or other cdn provider for live streaming service then this is very useful, becouse when you have many users who are streaming / viewing then you will have to get the closest CDN DNS redirection to them via JSONP document. But sense the url can be different depending on the end user location that would be hard to manage manually. This project solve that problem and automate everything for you so you don't have to focus on that anymore.


<b>How to use?</b>


1: Download the source folder, add the source and header file into your project folder:

<code>get_server.m</code><br>
<code>get_server.h</code>


2: import the header file inside your ViewController:

<code>#import "get_server.h"</code>

3: add the delegate to your ViewController:

<code>get_serverDelegate</code>

4: add the server state handler inside your ViewController to get notification about success, errors, timeout, finished, etc :<br>
```
- (void) get_server_finished:(NSString*)output error:(NSInteger)code{
    
    
    if (code == 1) {
        
        //succeed
        
        NSLog(@"%@",output);
        
    }else{
        
        switch (code) {
            case -1:
                NSLog(@"Source protocol not supported");
                break;
                
            case -2:
                //domain fail
                NSLog(@"%@",output);
                break;
                
            case -3:
                //404 error
                NSLog(@"%@",output);
                break;
                
            case -4:
                // timeout
                NSLog(@"%@",output);
                break;
                
            default:
                break;
        }
        
    }
    
    NSLog(@"Fetching data done...\n\n\n");
}
```


5:  Define the connection and active the delegate inside viewDidLoad:<br>

<code>
get_server * connection = [get_server new];
connection.delegate = self;
</code>


6: Let say your Service Identifier is <b>539462006</b>.r.cdnsun.net at CDNsun in this case add that line down below inside your viewDidLoad to connect and get the correct CDN DNS redirection:<br>

<code>
[connection send_request: [NSString stringWithFormat:@"https://video.worldcdn.net/539462006/%@.jsonp?callback=MyCallBack", @"streamname"] type:@"rtmp" timeout:1.5];
</code><br>

Type the correct stream name and as type you can choose one of the following protocols that you want to get: adobe, apple, rtsp, rtmpe or rtmp. You can also change the max value for timeout to anything. Debug and check the output of your console. There is also included example project to test out. Enjoy!

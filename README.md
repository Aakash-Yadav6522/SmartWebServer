# SmartWebServer
* An HTTP web server is a software application that handles HTTP (Hypertext Transfer Protocol) requests and responses. It serves web content to clients, typically web browsers, upon their request. When a user enters a URL in their web browser or clicks on a link, the browser sends an HTTP request to the web server, and the server responds by sending the requested content back to the client.The backbone of talented web server is socket programming/network programming available in built-in libraries such as arpa/inet.h & sys/socket.h.
# Features
* HTTP/1.1(Version 1.1) support.
* Supports GET/POST type Request.
* Supports static & dynamic mime type adding for any file format.
* Built-in encoding/decoding.
* Parser for Query strings in requests.
# Test Case
* Reference : /appOne 
```
//Bobby [The user]  
//Assume that the below code is being written by the server user
int main()
{
try
{
Bro bro;    //Creating Object of bro class
bro.setStaticResourcesFolder("whatever"); //whatever folder will containt all necessary files to be used
bro.get("/save_test1_data",[](Request &request,Response &response) void {
const char *html=R""""(
<!DOCTYPE HTML>
<html lang='en'>
<head>
<meta charset='utf-8'>
<title>Bro Test Cases</title>
</head>
<body>
<h1>Test Case 1-GET with Query string</h1>
<h3>Response From Server side</h3>
<b>Data Saved</b>
<br/><br/>
<a href='/index.html'>Home</a>
</body>
</html>
)"""";
response.setContentType("text/html");
response<<html;
});
bro.post("/save_test2_data",[](Request &request,Response &response) void {
const char *html=R""""(
<!DOCTYPE HTML>
<html lang='en'>
<head>
<meta charset='utf-8'>
<title>Bro Test Cases</title>
</head>
<body>
<h1>Test Case 2-POST with Form Data</h1>
<h3>Response From Server side</h3>
<b>Data Saved</b>
<br/><br/>
<a href='/index.html'>Home</a>
</body>
</html>
)"""";
response.setContentType("text/html");
response<<html;
});
bro.listen(6060,[](Error & error)void {
if(error.hasError())
{
cout<<"error.getError()";
return;
}
cout<<"Bro HTTP server is ready to accept request on port no. 6060"<<endl;
});
}catch(string exception)
{
//In case if something is not going as per the rule
cout<<exception<<endl;
}
return 0;
}

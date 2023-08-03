# SmartWebServer
* An HTTP web server is a software application that handles HTTP (Hypertext Transfer Protocol) requests and responses. It serves web content to clients, typically web browsers, upon their request. When a user enters a URL in their web browser or clicks on a link, the browser sends an HTTP request to the web server, and the server responds by sending the requested content back to the client.These servers play a vital role in hosting websites, serving web content, and facilitating communication between clients and servers on the World Wide Web.
# Features
* HTTP/1.1(Version 1.1) support.
* Supports GET type Request.
* Listrning and Accepting Connection.
* Content Serving.
* Request Handling.
# Test Case
#include<tmwp>  
#include<iostream>  
#include<stdlib.h>  
#include<ctime>  
using namespace std;  
using namespace tmwp;  
void dispatchTime(Request &request,Response &response)  
{  
time_t t=time(0);
char *now=ctime(&t);
response.write("<!DOCTYPE HTML>");
response.write("<html lang='en'>");
response.write("<head>");
response.write("<meta charset='utf-8'>");
response.write("<title>The Clock</title>");
response.write("</head>");
response.write("<body>");
response.write("<h1>");
response.write(now);
response.write("</h1>");
response.write("<a href='now'>Refresh</a><br>");
response.write("<a href='index.html'>Home</a><br>");
response.write("</body>");
response.write("</html>");
response.close();
}
void getCityView(Request &request,Response &response)
{
cout<<"getCityView is being process"<<endl;
string cityCodeString=request.get("cityCode");
cout<<"("<<cityCodeString<<")"<<endl;
int cityCode=atoi(cityCodeString.c_str());
if(cityCode==1) request.forward("Ujjain.html");
else if(cityCode==2) request.forward("Indore.html");
else if(cityCode==3) request.forward("Dewas.html");
else
{
request.setKeyValue("error","Invalid choice,City is not selcted");
request.forward("errorPage");
}
}
void createErrorPage(Request &request,Response &response)
{
string errorMessage=request.getValue("error");
response.write("<!DOCTYPE HTML>");
response.write("<html lang='en'>");
response.write("<head>");
response.write("<meta charset='utf-8'>");
response.write("<title>The Clock</title>");
response.write("</head>");
response.write("<body>");
response.write("<h1>");
response.write(errorMessage);
response.write("</h1>");
response.write("<a href='index.html'>Home</a><br>");
response.write("</body>");
response.write("</html>");
response.close();
}
void saveEnquiry(Request &request,Response &response)
{
string n=request.get("nm");
string c=request.get("ct");
string a=request.get("ad");
string m=request.get("msg");
cout<<"Request Received:"<<endl;
cout<<"Name: "<<n<<endl;
cout<<"City: "<<c<<endl;
cout<<"Address: "<<a<<endl;
cout<<"Query: "<<m<<endl;
//some logic to save data someWhere (maybe a file or some database)
request.forward("saveNotification.html");
}
int main()
{
TMWebProjector server(8080);
server.onRequest("/now",dispatchTime);
server.onRequest("/addEnquiry",saveEnquiry);
server.onRequest("/getCity",getCityView);
server.onRequest("/errorPage",createErrorPage);
server.start();
return 0;
}

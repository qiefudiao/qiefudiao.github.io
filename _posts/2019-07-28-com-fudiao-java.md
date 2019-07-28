---
layout: post
title: "servlet接受ajax传值"
date: Jul 19, 2019 9:21 PM
image: 'http://i1.fuimg.com/693111/c0ff6b9d25b28bf1.jpg'
description: servlet
tags:
- java
- data structure
twitter_text: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
introduction: JSP节课项目遇到的问题
---
# java后台接收一个formdata
需要注意，ajax传JSON时设置的content-type 如果是`application/json`或者`text/json`时，JAVA中`request.getParameter("")`是接收不到数据的,因为此时post的数据会已流的形式传输，可以使用`request.getInputStream()`来获得流,
此次结课项目中获取formdata的小例子：
```java
/*
getFilePath()函数
*/
//1、设置环境:创建一个DiskFileItemFactory工厂
DiskFileItemFactory factory = new DiskFileItemFactory();
//设置上传文件的临时目录
factory.setRepository(f1);
//2、核心操作类:创建一个文件上传解析器。
ServletFileUpload upload = new ServletFileUpload(factory);
//解决上传"文件名"的中文乱码
upload.setHeaderEncoding("UTF-8");
//4、使用ServletFileUpload解析器解析上传数据，解析结果返回一个List<FileItem>集合，每一个FileItem对应一个Form表单的输入项
List<FileItem> items =upload.parseRequest(request);

//如果fileitem中封装的是普通输入项的数据（输出名、值）
if(item.isFormField()){
String filedName = item.getFieldName();//普通输入项数据的名
//解决普通输入项的数据的中文乱码问题
String filedValue = item.getString("UTF-8");//普通输入项的值
System.out.println("普通字段:"+filedName+"=="+filedValue);
params.put(filedName, filedValue);
} //返回了JSON字符串
```
```java
Map params = GetFilePath.getFilePath(request);
String jsonMessage = params.get("data").toString(); //获取JSON字符串 data
JSONObject  myJson = JSONObject.fromObject(jsonMessage); //把string转化为JSONObject
Customer customer = (Customer) JSONObject.toBean(myJson,Customer.class); //处理JSONobject为customer
```
# java后台接收一个JSON字符串
上个例子获取formdata的时候其实已经处理了JSON字符串，下面是另一种方法处理JSON字符串
```java
/*
JsonReader.receivePost()
*/
public static JSONObject receivePost(HttpServletRequest request) throws IOException, UnsupportedEncodingException{

BufferedReader br = new BufferedReader(new InputStreamReader(request.getInputStream(),"utf-8")); //流的方式获取post的数据
String line = null;
StringBuilder sb = new StringBuilder(); //定义一个可变字符串
while((line=br.readLine())!=null) {
sb.append(line);  //依行读取
}
JSONObject json = JSONObject.fromObject(sb.toString()); 
return json; //返回JSONobject
}
```
```java
JSONObject myJson = JsonReader.receivePost(request);
String filePath = (String) myJson.get("url"); //使用key值就可取出value了
```
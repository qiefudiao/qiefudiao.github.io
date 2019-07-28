---
layout: post
title: "Ajax传值问题"
date: Jul 27, 2019 12:43 PM
image: 'http://i2.tiimg.com/693111/ede715271661cccc.jpg'
description: ajax
tags:
- java
- Ajax
twitter_text: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
introduction: JSP结课项目中遇到的Ajax问题
---
## Ajax向后台传数据
### 1.值类型为Formdata
html代码:
```
//ectype编码类型，ajax上传文件时可以不用设置;multiple允许上传多个文件
<form style="display:none;" action="" enctype="multipart/form-data" method="post"  id="fileupload">
	<input type="file" multiple  name="file1" id="file">
</form>
```
script代码:
```js
//获取form表单里的file
var form=$("#fileupload")[0];
//把file作为formData第一个值
var formdata = new FormData(form);
var data = {  //JSON格式
                name:name,
                source:source,
                status:status,
                sysUserId:sysUserId,
                telTime:telTime,
                estimateTime:estimateTime,
                money:money,
                address:address,
                phone:phone,
                remark:remark,
				}
//append添加第二个值JSON字符串
formdata.append("data",JSON.stringify(data));
```
Ajax代码:
```js
$.ajax({
			url:"customerServlet?method=save",
			type:"POST",
			cache: false,//上传文件无需缓存
	        processData: false,//用于对data参数进行序列化处理 这里必须false
	        contentType: false, //不设置编码类型
		    data:formdata,  //向后台传的值
		    success:function(result) {
            	alert("success");
            	if($("#conti").is(':checked')){
            		window.location.href="http://localhost:8080/CRM/customerEdit.jsp"; //跳转页面
            	}else{
            		window.location.href="http://localhost:8080/CRM/customerList.jsp";	
            	}
            },
            error:function(){
                    alert("error");
	        }
		});

```
####ajax属性添加的简要解释
contentType代表发送信息至服务器时内容编码类型,默认值为`contentType = "application/x-www-form-urlencoded"`
`contentType = false`在传输文件是的解释：
>Ajax封装了一个 formData 对象，然后使用 post 方法将文件传给服务器。
>这里我们就要先说说http中传输文件的问题。起初，http 协议中没有上传文件方面的功能，直到 rfc1867 为 http 协议添加了这个功能。当然在 rfc1867 中限定 form 的 method 必须为 POST ， ``enctype = "multipart/form-data"`` 以及``<input type = "file">``.
>当我们使用表单上传文件时，我们来查看他的Request headers：
>发现在 multipart/form-data 后面有boundary以及一串字符，这是分界符，后面的一堆字符串是随机生成的，目的是防止上传文件中出现分界符导致服务器无法正确识别文件起始位置。说到这肯定就要说说这分界符有啥作用呢？
>因为对于上传文件，我们没有使用原有的 http 协议，所以 multipart/form-data 请求是基于 http 原有的请求方式 post 而来的.那么来说说这个全新的请求方式与 post 的区别:
>请求头的不同，对于上传文件的请求，`contentType = multipart/form-data`是必须的，而 post 则不是，毕竟 post 又不是只上传文件。
>请求体不同。这里的不同也就是指前者在发送的每个字段内容之间必须要使用分界符来隔开，比如文件的内容和文本的内容就需要分隔开，不然服务器就没有办法正常地解析文件，而后者 post 当然就没有分界符直接以 `name = "value"`的形似发送。
>说到这，我们发现在 JQuery ajax() 方法中我们使contentType = false,这不是冲突了吗？这当然没有，因为当我们查看这时的 Request headers，会发现还是有分界符。这就是因为当我们在 form 标签中设置了`enctype = "multipart/form-data"`,这样请求中的 contentType 就会默认为 multipart/form-data 。而我们在 ajax 中 contentType 设置为 false 是为了避免 JQuery 对其操作，从而失去分界符，而使服务器不能正常解析文件。


###2.值类型为JSON.stringify()（JSON字符串）
Ajax代码
```js
$.ajax({
        url:"customerServlet?method=filedown",
        contentType: 'application/json',  //必须添加，否则后台收不到data
        type:'post',
        data:JSON.stringify(data),
        success:function (request) {
            $("#queryCourseForm").attr("action","customerServlet?method=downLoad");//改变表单的提交地址为下载的地址
            $("#queryCourseForm").submit();//提交表单
        }
    });
```


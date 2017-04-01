---
layout: post
title:  Python爬虫如何搞定反扒的403
category: blog
description: 一把辛酸泪
---

##1. 403的出现
媳妇想买个rimowa的箱子，于是早上就动心写个小虫子，扒一扒smzdm的搜索结果

    import requests
    url = 'http://search.smzdm.com/?c=home&s=rimowa'
    html = requests.get(url).text

html并没有按预期显示任何内容，而是很多的乱码。

    <div class="online-desc-con" style="width:550px;padding-top:15px;margin:34px auto;">
    <a id="official_site" href="//www.yunaq.com" target="_blank">
    <img alt="" style="margin: 0 auto 17px auto;" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAG4AAABuCAYAAAGxXBZtAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyJpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuMy1jMDExIDY2LjE0NTY2MSwgMjAxMi8wMi8wNi0xNDo1NjoyNyAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENTNiAoV2luZG93cykiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6RDMwMzQxQUY2NDVEMTFFMjkxQzRFMDgyREMzQjIyNzMiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6RDMwMzQxQjA2NDVEMTFFMjkxQzRFMDgyREMzQjIyNzMiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDpEMzAzNDFBRDY0NUQxMUUyOTFDNEUwODJEQzNCMjI3MyIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDpEMzAzNDFBRTY0NUQxMUUyOTFDNEUwODJEQzNCMjI3MyIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PvX1efcAACeISURBVHjalFI9TwJBEH17OSPERE3AyoaESkr/AxRySgIYExKhAKSk1VDQaUdoKNCj40hAYogChWiM/8CGRApCR0GllUrubmUXb5WPxk3mdjMz783cmyH+oh//

打印了一下errorcode是403
之前听说过有些网站做了反扒，所以开始怀疑是这个原因

##2. 给Requests加headers
熟悉http协议的都知道header标识了访问者的身份。
一个常见的header可以这么写

    headers = { "Accept":"text/html,application/xhtml+xml,application/xml;",
                "Accept-Encoding":"gzip",
                "Accept-Language":"zh-CN,zh;q=0.8",
                "Referer":"http://www.example.com/",
                "User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.90 Safari/537.36" }

然后在Requests中使用上面定义的headers

    response = requests.get(url,headers)
    pageHtml = response.text

然后又华丽丽的依然不成功。。。

![403pic](http://upload-images.jianshu.io/upload_images/3587181-efe658830e2277d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##3. 原因
仔细检查到底是什么问题，原来是requests调用headers的方法错了，这里要特别注意

    response = requests.get(url,headers=headers)

至此，可以识别出来反扒的smzdm了，撒花





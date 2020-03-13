---
layout: post
title: 网络测试
permalink: /speedtest.html
---

## 延时测试

<script type="text/javascript"
src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js">
</script>

<script>
$.ping = function(option) 
{
    var ping, requestTime, responseTime ;
    $.ajax({
        url: option.url+'/speed_test'+ (new Date()).getTime() + '.html',
        type: 'GET',
        dataType: 'html',
        timeout: 10000,
        beforeSend : function() 
        {
            if(option.beforePing) option.beforePing();
            requestTime = new Date().getTime();
        },
        complete : function() 
        {
            responseTime = new Date().getTime();
            ping = Math.abs(requestTime - responseTime);
            if(option.afterPing) option.afterPing(ping);
        }
    });
    if(option.interval && option.interval > 0)
    {
        var interval = option.interval * 1000;
        setTimeout(function(){$.ping(option)}, interval);
    }
};
</script>

<div id="msg"></div>
<script type="text/javascript">
$.ping({
url : 'https://blog.chgtaxihe.top', 
beforePing : function(){$('#msg').html('正在计算延迟')},
afterPing : function(ping){$('#msg').html('您到本站的延迟为' + ping + 'ms')}, 
interval : 10
});
</script>

[100M测速文件](http://speedtest-sgp1.digitalocean.com/100mb.test)


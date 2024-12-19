---
comments: false
statistics: True
hide:
  - feedback
---

# Welcome to Melody's notebook!

!!! note "" 
    <br><br>
    <div align="center" style="font-size:32px;font-weight:bold">
        允许一切发生，但只解决问题。
    </div>
     <br><br>

!!! info ":material-chart-line: 站点统计"
    <center>
    页面总数：{{pages}}  
    总字数：{{words}}  
    代码块行数：{{codes}}  
    网站运行时间：<span id="web-time"></span>
    </center>

这是一个记录我学习过程和笔记的网站，浅陋之见，伏侯卓裁。

学习过程中难免犯错，如果发现了什么错误，欢迎在评论区留言，或者通过邮箱(Melody12020831@outlook.com)联系我。

本项目的许可证为 <!--[![CC BY-NC-SA Logo](https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png) -->[知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)

<script>
function updateTime() {
    var date = new Date();
    var now = date.getTime();
    var startDate = new Date("2024/11/20 21:22:28");
    var start = startDate.getTime();
    var diff = now - start;
    var y, d, h, m;
    y = Math.floor(diff / (365 * 24 * 3600 * 1000));
    diff -= y * 365 * 24 * 3600 * 1000;
    d = Math.floor(diff / (24 * 3600 * 1000));
    h = Math.floor(diff / (3600 * 1000) % 24);
    m = Math.floor(diff / (60 * 1000) % 60);
    if (y == 0) {
        document.getElementById("web-time").innerHTML = d + "<span class=\"heti-spacing\"> </span>天<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>小时<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>分钟";
    } else {
        document.getElementById("web-time").innerHTML = y + "<span class=\"heti-spacing\"> </span>年<span class=\"heti-spacing\"> </span>" + d + "<span class=\"heti-spacing\"> </span>天<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>小时<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>分钟";
    }
    setTimeout(updateTime, 1000 * 60);
}
updateTime();
function toggle_statistics() {
    var statistics = document.getElementById("statistics");
    if (statistics.style.opacity == 0) {
        statistics.style.opacity = 1;
    } else {
        statistics.style.opacity = 0;
    }
}
</script>
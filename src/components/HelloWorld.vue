<template>
    <div id="box">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
        </ul>
    </div>
</template>

<script>
import hammer from 'hammerjs';
export default {
    name: 'HelloWorld',
    data () {
        return {
          msg: ''
        }
    },
    mounted (){
        var _w = $('body').width();
        $('li').width(_w);
        console.log(_w);
        var hammertime = new Hammer(document.getElementById("box"));
        var num = 1;
        //向右滑动，上一张
        hammertime.on("swiperight", function(e) {
            console.log("向右滑动，上一张"+ num);
            if(num<1){return false};
            var left = _w * (num-2);
            $("ul").css('transform', 'translateX(-' + left + 'px)');
            num--;
        });
        // 向左滑动，下一张
        hammertime.on("swipeleft", function(e) {
            console.log("向左滑动，下一张"+num);
            if(num>4){return false};
            var left = _w * num;
            $("ul").css('transform', 'translateX(-' + left + 'px)');
            num++;
        });
    }
}
</script>
<style scoped>
#box{
    width:100%;
    height:100%;
    overflow-x:auto;
}
ul{
    width:auto;
    height:100%;
    overflow: visible;
    white-space: nowrap;
    font-size:0;
}
ul li{
    display:inline-block;
    height:100%;
    background:#FFCCCC;
    text-align: center;
    color:#fff;
    line-height:500px;
    font-size:60px;
}
li:nth-of-type(2n){
    background:#CC9999;
}
</style>

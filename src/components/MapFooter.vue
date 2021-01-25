<template>
  <div class="footer">
      <div class="left">@京2021 SJRE</div>
      <div class="right">
          /// {{this.nowTime}}
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            nowTime: new Date(),
            intervalId: null
        }
    },
    methods:{
        dateFormat(fmt, date) {
            let ret;
            const opt = {
                "Y+": date.getFullYear().toString(),        // 年
                "m+": (date.getMonth() + 1).toString(),     // 月
                "d+": date.getDate().toString(),            // 日
                "H+": date.getHours().toString(),           // 时
                "M+": date.getMinutes().toString(),         // 分
                "S+": date.getSeconds().toString()          // 秒
                // 有其他格式化字符需求可以继续添加，必须转化成字符串
            };
            for (let k in opt) {
                ret = new RegExp("(" + k + ")").exec(fmt);
                if (ret) {
                    fmt = fmt.replace(ret[1], (ret[1].length == 1) ? (opt[k]) : (opt[k].padStart(ret[1].length, "0")))
                }
            }
            return fmt
        },
        initData(){
            let date = new Date();
            this.dateFormat("YYYY-mm-dd HH:MM:SS", date)
            this.nowTime = this.dateFormat("YYYY-mm-dd HH:MM:SS", date);
        },
        // 定时刷新数据函数
        dataRefreh() {
            // 计时器正在进行中，退出函数
            if (this.intervalId != null) {
                return;
            }
            // 计时器为空，操作
            this.intervalId = setInterval(() => {
                // console.log("刷新" + this.nowTime);
                this.initData(); //加载数据函数
            }, 10);
        }, 
        // 停止定时器
        clear() {
            clearInterval(this.intervalId); //清除计时器
            this.intervalId = null; //设置为null
        },
    },
    created(){
        this.dataRefreh();
    },
    destroyed(){
        // 在页面销毁后，清除计时器
        this.clear();
    }
}
</script>

<style scoped>
    .footer{
        display: flex;
        color: #fff;
    }
    .right{
        position: fixed;
        right: 10px;
    }
</style>
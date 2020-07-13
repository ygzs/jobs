一   uni-app多种设置全局变量及全局变量重新赋值

1. 公用模块
    <pre>
    定义一个专用的模块，用来组织和管理这些全局的变量，在需要的页面引入。
    注意这种方式只支持多个vue页面或多个nvue页面之间公用，vue和nvue之间不公用。
    </pre>
    引用公共common.js
    ```javascript
        export default {
            memberObj:{
            name:'初始姓名',
            },
            setMemberObj(data){
                this.memberObj = Object.assign({},this.memberObj,data) 
            }
        }
    ```
    在全局main.js中引用
    ```javascript
        //...
        import member from './common/common.js'
        //...
        Vue.prototype.$member = member;
        //...
    ```
    在普通页面获取全局变量，重新赋值
    ```javascript
        onShow:function(){
            //获取全局设置的变量
            this.memberData = this.$member.memberObj;
            console.log(this.memberData);
            //输出值{name:'初始姓名'}
        },
        methods: {
            bindLogin() {
                let that = this;
                let obj = {
                    name:'爱尚',
                    sex:'男'
                }
                that.$member.setMemberObj(obj);
            },
        }
        //再次在别的页面调用时内容已发生变化
        console.log(this.$member.memberObj)
        //{name:'爱尚',sex:'男'}
    ```

2.  挂载 Vue.prototype
    <pre>
    将一些使用频率较高的常量或者方法，直接扩展到 Vue.prototype 上，每个 Vue 对象都会“继承”下来。
    注意这种方式只支持vue页面
    </pre>
    在 main.js 中挂载属性/方法
    ```javascript
        Vue.prototype.websiteUrl = 'http://uniapp.dcloud.io';  
        Vue.prototype.now = Date.now || function () {  
            return new Date().getTime();  
        }; 
    ```
    然后在 pages/index/index.vue 中调用
     ```javascript 
        export default {  
            data() {  
                return {};  
            },  
            onLoad(){  
                console.log('now:' + this.now());  
            },  
            methods: { }  
        }   
    ```

3.  globalData在小程序中

4.  vuex

<pre>
转载于： https://ask.dcloud.net.cn/article/35021
        https://www.cnblogs.com/aishangliming/p/10959497.html
</pre>


二  the second day

1.  <pre>Math.floor(x) 返回小于等于 x 的最大整数</pre>

2.  <pre>标签的 disabled 属性规定应该禁用 input 元素</pre>

3.  <pre>
    @blur 是当元素失去焦点时所触发的事件
    失去焦点就是指当前元素里没有鼠标的光标.
    </pre>

4.  uni-app两种提示框
    <pre>
    uni.showToast(OBJECT)
    uni.showModal(OBJECT)
    </pre>


三 the forth day

1.  input 标签
    <pre>
    checked 属性规定在页面加载时应该被预先选定的 input 元素。
    checked 属性 与  input type="checkbox"  或  input type="radio" 配合使用。
    checked 属性也可以在页面加载后，通过 JavaScript 代码进行设置。
    </pre>


四 The fifth day

1.  <pre>
    在每次登录成功后获取当前时间戳 currentTime，（Math.round(new Date() / 1000) ），存储到localStorage中，同时从后台返回一个到期时间 endTime，当 currentTime < endTime 时，用户无需重复登录
    </pre>


五 2020/06/15

1.  uniapp自定义导航栏返回按钮及点击事件 
    ```javascript
    onBackPress(options) {
        if (options.from === 'navigateBack') {
        return false;
        }
        uni.reLaunch({
            url: 'index'
        });
        return true;
    },
    // 返回上一页
    ```
2.  uni-app 上传图片可以不用设置 header


六 2020/06/16

1.  [object Object]
    <pre>
    默认情况下，toString()方法被每个Object对象继承。如果此方法在自定义对象中未被覆盖，toString()返回 "[object type]"，其中type是对象的类型。
    可以先用 JSON.stringify( ) 转换一下
    </pre>


七 2020/06/17

1.  html5页面简单判断当前有无网络
    ```javascript
    if (navigator.onLine) { 
        alert('online'); 
    } else { 
        alert('offline'); 
    }

    window.addEventListener('offline', function(e) {alert('offline');}) 
    window.addEventListener('online', function(e) {alert('online``');}) 
    ```
    参考：https://blog.csdn.net/junoohoome/article/details/51850134

    
八 2020/06/21

1.  如何让 button 标签中的文字居中
    给文字设置line-height，等于button高度。

2.  flex-wrap: wrap
    让弹性盒元素在必要的时候拆行。


九 2020/06/22

1.  一般在注册页面，在 form 表单的其中一行有
    ```html
    <form>
        <div class="row">
            <span>用户名</span>
            <input type="text" placeholder="请输入用户名">
        </div>
        <div class="row">
            <span>手机号</span>
            <input type="number" placeholder="请输入手机号">
            <p>获取验证码</p>
        </div>
    </form>
    ```
    ```css
    .row{
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
    .row > span{
        width: 4em;
    }
    .row > input{
        flex-grow: 1;
    }
    .row > p{
        display: inline-block;
    }
    .row:nth-child(2) > input{
        width: 1px;
    }
    ```

2.  tab 切换
    ```html
     <div id="app">
        <ul class="tab-tit">
            <li v-for="(title,index) in tabTitle" @click="cur=index" :class="{active:cur==index}">{{title}}</li>
        </ul>
        <div class="tab-content">
            <div v-for="(m,index) in tabMain" v-show="cur==index">{{m}}</div>
        </div>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el:'#app',
            data:{
                tabTitle: ['标题一', '标题二', '标题三', '标题四'],
                tabMain: ['内容一', '内容二', '内容三', '内容四'],
                cur: 0 //默认选中第一个tab
            }
        })
    </script>
    ```

十 2020/06/23

1.  在 hbuilderx 打包为 h5 后，可以用外壳打包为 apk 或者 ipa ，ipa 为越狱版，然后用 appcake 安装到没有越狱的 iPhone 上


十一 2020/06/28

1.  ```json
    "path": "pages/index/index",
    "style": {
        "navigationStyle":"custom",
        "app-plus":{
            "titleView":false  
        }  
    }
    ```
    设置单页面去除原生导航栏
    参考：https://www.cnblogs.com/ruruo/p/11544630.html
    参考：https://www.cnblogs.com/li-sir/p/12155267.html

2.  ```javascript
    created(){
        if(this.information.type === 2){
            uni.setTabBarItem({
                index: 1,
                text: '简历',
            })
        }
    },
    ```
    在页面中动态设置tabBar

3.  <pre>
    created  模板还没有被渲染成html，这时候通过id什么的去查找页面元素是找不到的

    mounted  挂载完成以后也就是模板渲染完成以后才会被调用。

    computed是属性调用，而methods是函数调用
    computed带有缓存功能，而methods不是

    computed定义的方法我们是以属性访问的形式调用的，{{computedTest}}
    但是methods定义的方法，我们必须要加上()来调用，如{{methodTest()}}

    页面加载完成后执行  onload
    </pre>


十二 2020/06/30

1.  vue watch监听对象及对应值的变化
    ```javascript
    var vm=new Vue({
        data:{
            a:1,
            b:{
                c:1
            }
        },
        watch:{
            a(val, oldVal){//普通的watch监听
                console.log("a: "+val, oldVal);
            },
            b:{//深度监听，可监听到对象、数组的变化
                handler(val, oldVal){
                    console.log("b.c: "+val.c, oldVal.c);//但是这两个值打印出来却都是一样的
                },
                deep:true
            }
        }
        })
    vm.a=2
    vm.b.c=2
    ```
    参考：https://blog.csdn.net/qq_17757973/article/details/78721553

2.  JS如何判断一个数组里面的所有值相等（只针对数字）
    <pre>
    判断数组中最大值和最小值是否相等
    简单数组
    const arr = [1,2,3,4,5,6,7]
    Math.max.apply(null, arr) === Math.min.apply(null, arr)
    对象数组，其实就是把对象数组转换成简单数组
    const obj = [{id:1,price:1.5},{id:2,price:1.5}]
    const arr = obj.map(o=>o.price)
    Math.max.apply(null, arr) === Math.min.apply(null, arr)

    参考：https://blog.csdn.net/thorLei/article/details/83148966
    </pre>

3.  获取地理位置的信息
    ```javascript
    navigator.geolocation.getCurrentPosition(success, error, options)
    ```

十三  2020/07/01

1.  <pre>
    需要使用自定义模板的场景，通常有以下几种情况：
        调整页面 head 中的 meta 配置 
        补充 SEO 相关的一些配置（仅首页） 
        加入百度统计等三方js 
        
        使用自定义模板时，
        1. 工程根目录下新建一个html文件；
        2. 复制下面的基本模板内容，到这个html文件，在此基础上修改meta和引入js；
        3. 在 manifest.json->h5->template 节点中关联这个html文件的路径。
    </pre>

2.  uni-app 如何在当前页调上个页面的方法
    ```javascript
    var pages = getCurrentPages();//当前页
    var prevPage = pages[pages.length - 2];//上个页面
    // #ifdef H5
    beforePage.submitAct()
    // #endif
    // #ifndef H5
    beforePage.$vm.submitAct()
    // #endif
    ```

3.  子页面返回父页面，父页面刷新
    ```javascript
    //子页面
    let pages = getCurrentPages()
    let currPage = pages[pages.length - 1]
    let prevPage = pages[pages.length - 2]
    //prevPage.onLoad()
    prevPage._data.isDoRefresh = true
    uni.navigateBack({
        delta: 1,
    })

    //父页面
    if(this.isDoRefresh === true){
        //console.log(2)
        this.isDoRefresh = false
        this.checkInfo()
    }     
    ```

十四 2020/07/02

1.  取消原生导航栏的默认返回按钮：
    ```javascript
    mounted() {
        document.getElementsByClassName('uni-page-head-hd')[0].firstChild.style.display = 'none'
    },
    ```

2.  input 设置高度要先设置 background-color 再设置 height

3.  页面间通讯
    ```javascript
    var Event=new Vue()
    Event.$emit('update',{msg:'页面更新'})
    Event.$on('update',(data) => {
        console.log(data.msg)
    })
    ```

十五 2020/07/04

1.  <pre>
    小程序 v-show 是通过伪类 view[hidden]{display:none} 实现，用户写的 display: flex 权重较高，使之失效。可以改成 v-if。
    </pre>

十六 2020/07/06

1.  使用 $.emit 和 $.on 传递参数，第一次 $.on 不执行
    ```javascript
    //在 main.js 中
    Vue.prototype.$EventBus = new Vue({
        data () {
            return {
                content: '',
            }
        },
        created(){
            this.$once('update', (data)=>{
                this.content = data
            })
        }
    })

    //在数据发出页面
    this.$EventBus.$emit('update','xxxx');
    
    //在数据接收页面
    this.updateContent = this.$EventBus.content
    ```

2.  微信小程序中点击事件传递参数
    <pre>
    首先 @click 绑定点击事件，
    在标签中利用 data-xxx  来定义你要传入的参数，，
    然后事件中传入 event 用 event.currentTarget.dataset.xxx 来取你传入的值
    </pre>
    ```html
    <li v-for='(item,index) in news' :key='index' @click='VXreadNews' :data-s='item'>
    ```
    ```javascript
    VXreadNews(e){
        let content = e.currentTarget.dataset.s
    }
    ```

十七 2020/07/08

1.  placeholder 换行
    ```
    &#13; 表示回车
    &#10;表示换行
    ```

2.  form 中 @submit ，必须有 name 才能获取相应的值

十八 2020/07/09

1.  uni-app 原生导航栏返回事件
    ```javascript
    onBackPress(e) {
        if (e.from === 'navigateBack') {  
            return false  
        }  
        this.back()
        return true
    },
    methods: {
        back(){
            uni.navigateBack({  
                delta: 2  
            })
        }
    }
    ```

2.  外部 div 完全包裹住内部 img 并使图片居中
    ```css
    .wapper{
        text-align: center;
    }
    .wapper > img{
        vertical-align: top;
    }
    ```

十九 2020//07/12

1.  如何让div中的文字只显示一行，多余的文字隐藏并加上省略号
    ```css
    div{
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
    }
    ```

二十 2020/07/13

1.  vue实现消息的无缝滚动效果
    ```javascript
    export default {
        data() {
            return {
                animate:false,
                items:[
                    {name:"小明"},
                    {name:"小红"},
                    {name:"小刚"}
                ]
            }
        },
        created(){
            setInterval(this.scroll,1000)
        },
        methods: {
            scroll(){
                this.animate=true;    // 因为在消息向上滚动的时候需要添加css3过渡动画，所以这里需要设置true
                setTimeout(()=>{      //  这里直接使用了es6的箭头函数，省去了处理this指向偏移问题，代码也比之前简化了很多
                    this.items.push(this.items[0]);  // 将数组的第一个元素添加到数组的
                    this.items.shift();               //删除数组的第一个元素
                    this.animate=false;  // margin-top 为0 的时候取消过渡动画，实现无缝滚动
                },500)
            }
        }
    }
    ```
    ```css
    #box{
        width: 300px;
        height: 32px;
        overflow: hidden;
        padding-left: 30px;
        border: 1px solid black;
    }
    .anim{
        transition: all 0.5s;
        margin-top: -30px;
    }
    #con1 li{
        list-style: none;
        line-height: 30px;
        height: 30px;
    }
    ```
    ```html
    <div id="box">
        <ul id="con1" ref="con1" :class="{anim:animate==true}">
            <li v-for='item in items'>{{item.name}}</li>
        </ul>
    </div>
    ```
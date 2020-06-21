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
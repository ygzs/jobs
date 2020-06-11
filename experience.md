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

2.  
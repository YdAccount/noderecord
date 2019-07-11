# Vue

1. ```javascript
   模板
   <template>
       //包含一个根元素
       <div>
      {{msg}}
      <v-header></v-header>
      <v-footer></v-footer>
       </div>
   </template>
   <script>
       import Header from '../... 
   	import Footer from '../....'
       export default {
           day (){
               return {
                   msg:'nihao',
               }      
           },
           components:{
               'v-header':Header,
               "v-footer":Footer
           }，
           methods:{  }，
        //生命周期函数
       beforemMount（）{
           模板编译之前
       }，
       mounted(){
           模板编译完成，请求数据。操作dom都在这里
       }，
       beforeUpdata（）{数据更新之前}，
       updated（）{数据更新完毕}，
       beforeDestroy（）{页面销毁的时候要保存一些数据，就可以监听这个销毁的生命周期函数}，
       destoryed（）{实例销毁完毕}
       }
</script>
   <style></style>
   ```
   
2. 生命周期函数

   2.1  组件挂载。以及组件更新、销毁时触发的这一系列方法，这些方法叫做生命周期函数

   2.1.1函数在上

3. 请求数据模板：第三方插件v-resource

   3.1 `npm i v-resource`

   `main.js`中引入`vueResource = ‘’‘--》`挂载’,

   ```javascript
   getData(){
       this.$http.get(url).then(res=>{
            
       })
   }
   mounted(){
       this.getData(),进来页面就刷新数据，钩子函数
   }
   ```

   4.请求数据的模板`axios`

   5 . 父子组件传值

   5.1	父组件传子组件：给子组件动态绑定属性`;title="title",`在子组件里接收父组件传来的数据.

   <home>

   <v-son :title='456'> </v-son>

   </home>

   子组件：data同级下，props:['title']

   6 父组件主动获取子组件的数据和方法

   ``` javascript
   1调用子组件的时定义一个ref
   <v-header ref='header'></v-header>
   2.在父组件里通过
   this.$ref.header.属性/方法
   ```

   

7. 子组件主动获取父组件的数据和方法

   `this.$parent.数据/方法

5. 非父子组件传值

   ```javascript
   1. 新建一个js文件
   2.里面引入一个空的Vue：import Vue from 'vue'
   3. var vM=new Vue() //new一个实例
   4.暴露出去
   5.在需要的组件引入这个js文件，广播数据  （import vM from '../..'）
   vM.$emit('mingzi');
   ---------------
      另一个组件接收(先引入js文件),在mounted里vM.$on('mingi',(data=>{
       
   }))
   ```

   

   ## `day2 -p4`

   1.switch-开关状态改变 --状态改变事件

   1.1   change事件
   
   ```javascript
   <template slot-scop="scope">
       <switch @change="delState(scope)"><switch>
    </template>
   <script>
           delState(scope){
           axios({
               url:'/users/${scope.row.id/stste/${scope.row....}}',
     		 method:'post',      
           }).then(res=>{
      if (){alert('chenggong成功')}
      else{
          this.listData[scope.$index].mg_state=!scope.row.mg_state
            //取反--->数据接口请求失败，状态不变
           })
       }
    </script>
   
   ```
   
   
   
   ## `axios`配置
   
   ```javascript
   {
     // `url` 是用于请求的服务器 URL
     url: '/user',
   
     // `method` 是创建请求时使用的方法
     method: 'get', // 默认是 get
   
     // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
     // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
     baseURL: 'https://some-domain.com/api/',
   
     // `transformRequest` 允许在向服务器发送前，修改请求数据
     // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
     // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
     transformRequest: [function (data) {
       // 对 data 进行任意转换处理
   
       return data;
     }],
   
     // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
     transformResponse: [function (data) {
       // 对 data 进行任意转换处理
   
       return data;
     }],
   
     // `headers` 是即将被发送的自定义请求头
     headers: {'X-Requested-With': 'XMLHttpRequest'},
   
     // `params` 是即将与请求一起发送的 URL 参数
     // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
     params: {
       ID: 12345
     },
   
     // `paramsSerializer` 是一个负责 `params` 序列化的函数
     // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
     paramsSerializer: function(params) {
       return Qs.stringify(params, {arrayFormat: 'brackets'})
     },
   
     // `data` 是作为请求主体被发送的数据
     // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
     // 在没有设置 `transformRequest` 时，必须是以下类型之一：
     // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
     // - 浏览器专属：FormData, File, Blob
     // - Node 专属： Stream
     data: {
       firstName: 'Fred'
     },
   
     // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
     // 如果请求话费了超过 `timeout` 的时间，请求将被中断
     timeout: 1000,
   
     // `withCredentials` 表示跨域请求时是否需要使用凭证
     withCredentials: false, // 默认的
   
     // `adapter` 允许自定义处理请求，以使测试更轻松
     // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
     adapter: function (config) {
       /* ... */
     },
   
     // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
     // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
     auth: {
       username: 'janedoe',
       password: 's00pers3cret'
     },
   
     // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
     responseType: 'json', // 默认的
   
     // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
     xsrfCookieName: 'XSRF-TOKEN', // default
   
     // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
     xsrfHeaderName: 'X-XSRF-TOKEN', // 默认的
   
     // `onUploadProgress` 允许为上传处理进度事件
     onUploadProgress: function (progressEvent) {
       // 对原生进度事件的处理
     },
   
     // `onDownloadProgress` 允许为下载处理进度事件
     onDownloadProgress: function (progressEvent) {
       // 对原生进度事件的处理
     },
   
     // `maxContentLength` 定义允许的响应内容的最大尺寸
     maxContentLength: 2000,
   
     // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
     validateStatus: function (status) {
       return status >= 200 && status < 300; // 默认的
     },
   
     // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
     // 如果设置为0，将不会 follow 任何重定向
     maxRedirects: 5, // 默认的
   
     // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
     // `keepAlive` 默认没有启用
     httpAgent: new http.Agent({ keepAlive: true }),
     httpsAgent: new https.Agent({ keepAlive: true }),
   
     // 'proxy' 定义代理服务器的主机名称和端口
     // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
     // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
     proxy: {
       host: '127.0.0.1',
       port: 9000,
       auth: : {
         username: 'mikeymike',
         password: 'rapunz3l'
       }
     },
   
     // `cancelToken` 指定用于取消请求的 cancel token
     // （查看后面的 Cancellation 这节了解更多）
     cancelToken: new CancelToken(function (cancel) {
     })
   }
   ```
   
   ## 登录
   
   1. ```javascript
      保存token：window.localstorage.setItem(token,'shuju')
      ```
   
      2. ```javascript
         进入到主页时判断是否有token   ---获取token，getItem ***有问题（token接口）
         ```
      

2. ##分配角色

2.1  点击按钮-->发送请求获取所有角色列表

##   上传图片

```javascript
 <input @change="onUpload">

onUpload(e) {
                let files = e.target.files || e.dataTransfer.files;
                if (!files) return;
                // 临时凭证
                receive({
                    stsType: '10'
                })
                    .then(res => {
                        console.log(res);
                        if (res.rspCd === '00000') {
                            let endpoint = res.data.endpoint.substring(0, 15);
                            const client = new OSS({
                                region: endpoint,
                                accessKeyId: res.data.accesskeyid,
                                accessKeySecret: res.data.accesskeysecret,
                                stsToken: res.data.securitytoken,
                                bucket: res.data.bucketName
                            });
                            for (let i = 0; i < files.length; i++) {
                                const storeAs = res.data.url + '/' + files[i].name;
                                client
                                    .multipartUpload(storeAs, files[i], {})
                                    .then(res => {
//
                                        this.btnShow = false;
                                        this.imgShow = true;
                                        this.imgShowUrl.push(res.res.requestUrls[0]);
                                        console.log(this.imgShowUrl);
                                    })
                                    .catch(err => {
                                        console.log(err);
                                    });
                            }
                        }
                    })
                    .finally(() => {
                        this.loading = false;
                    });
            },
```

## day1

1. 计算属性computed&&监视watch

   ```javascript
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
       <script src="./node_modules/vue/dist/vue.js"></script>
   </head>
   <body>
        <div id="app">
            <input type="text" v-model="firstName">
         <input type="text" v-model="lastName">
            <input type="text" v-model="fullName" placeholder="全名">
            <br>
            <hr>
            <input type="text" v-model="fullName1" placeholder="双向">
        </div>
   </body>
   <script>
    const vm = new Vue({
           el:"#app",
           data:{
               firstName:'1',
               lastName:'1'
           },
           //计算属性
           computed:{
               fullName(){
                   return this.firstName +" " + this.lastName;
               },
                   //双向
               fullName1:{
   //                需要读取时调用并返回
                   get(){
                           return this.firstName + ' ' + this.lastName;
                   },
   //                  监视当前属性值变化
                   set(value){
                       const names= value.split(' ');
                       this.firstName= names[0]
                       this.lastName= names[1]
                   }
               }
   
   
           },
   //        监视①
           watch:{
               firstName(newValue,oldValue){
                   console.log("12")
                     return newValue + " " +this.lastName;
               }
           },
   
       })
          // 监视②
       vm.$watch("lastName",function (newValue) {
           console.log('56')
           return this.firstName+ " " + this.newValue;
       })
   </script>
   </html>
   ```
   
   2.列表的搜索和排序
   
   ```javascript
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
       <script src="./node_modules/vue/dist/vue.js"></script>
   </head>
   <body>
   <div id="app">
       <input type="text" v-model="searchCon">
       <ul>
           <li v-for="(item,index) in fliterPerson" :key="index">
               {{index}}----{{item.name}}----{{item.age}}
           </li>
       </ul>
   
       <button @click="setOrder(1)">年龄升序</button>
       <button @click="setOrder(2)">年龄降序</button>
       <button @click="setOrder(0)">年龄原序</button>
   </div>
   </body>
   <script>
       new Vue({
           el: "#app",
           data: {
               searchCon: '',
               orderType: '0',// 1 升序，2降序
               persons: [
                   {name: "tom", age: 15},
                   {name: "toom", age: 17},
                   {name: "jack", age: 16},
                   {name: "jjs", age: 20},
                   {name: "plo", age: 22},
               ]
           },
           computed: {
   //            搜索过滤
               fliterPerson() {
                   //取出需要数据
                   const {searchCon, persons, orderType} = this;
                   let res = persons.filter(val => val.name.indexOf(searchCon) !== -1)
                   if (orderType !== 0) {
                       res.sort(function (a, b) {
   //                        升序
                           if (orderType === 1) {
                               return a.age - b.age;
                           } else {
   //                            降序
                               return b.age - a.age;
                           }
                       })
                   }
                   return res
               }
           },
           methods: {
               setOrder(val) {
   
                   this.orderType = val;
               }
           }
           
       })
   
   </script>
   </html>
   ```
   
   3. vue 事件处理
   
      ```javascript
      1.事件修饰符
      @click.stop="test"   //.stop可阻止事件冒泡
      @click.prevent= 'test'  //.prevent阻止事件默认行为（a链接）
      
      2.按键修饰符
      @keyup.enter/.13 = "teat"  // 只有少量有
      
      
      ```
   
      4. 使用v-model收集表单数据
   
         ```javascript
         <!DOCTYPE html>
         <html lang="en">
         <head>
             <meta charset="UTF-8">
             <title>Title</title>
             <script src="./node_modules/vue/dist/vue.js"></script>
         </head>
         <body>
         <div id="app">
             <form action="/xxx">
                 <label for="name">姓名：<input type="text" id="name" v-model="user"></label>
                 <br>
                 <label for="pwd">密码：<input type="password" id="pwd" v-model="pwd"></label>
                 <br>
                 <label for="age">年龄：<input type="text" id="age" v-model="age"></label>
                 <br>
                 性别： <input type="radio" value="男" v-model="sex">男
                 <input type="radio" value="女" v-model="sex">女
                 <br>
                 爱好：<input type="checkbox" value="basktball" v-model="likes"> 篮球
                 <input type="checkbox" value="football" v-model="likes"> 足球
                 <input type="checkbox" value="football1" v-model="likes">足球1
                 <br>
                 城市：<select v-model="cityId">
                 <option value=" ">未选择</option>
                 <option :value="item.id" v-for="(item,index) in allCitys">{{item.city}}</option>
             </select>
                 <br>
                 <br>
                 <input type="submit" value="提交" @click.prevent="go">
             </form>
         </div>
         </body>
         <script>
             new Vue({
                 el: "#app",
                 data: {
                     user: '',
                     pwd: '',
                     age: '',
                     sex: "女", //默认选择女
                     likes: ["football"], //默认足球
         //          cityId:' ',
                     cityId: '3', //默认 长沙
                     allCitys: [
                         {id: '1', city: "bj"},
                         {id: '2', city: "gd"},
                         {id: '3', city: "cs"}
                     ]
                 },
                 methods: {
                     go() {
                         console.log(this.cityId)
                     }
                 }
             })
         
         </script>
         </html>
         ```
   
         5. Vue生命周期
   
            ```javascript
            
            ```
   
            
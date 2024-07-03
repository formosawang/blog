1. slot的应用场景，印象最深的，这两样看的最多的可能就是组件的封装了，运用slot来占位，来自定义自己想要展示的内容，也就是这两天，可能才知道了组件的封装是怎么回事，知道了那些开源的框架组件是怎
么封装的，是怎么通过属性来定义我们自己想要的内容的，父组件中的 v-slot:title就等价于#title，还等价于slot='title',给我的感觉是这样，就看自己怎用了，这个是具名插槽，那么在子组件中，就会找到对
应的名字，从而把父组件中的自定义的内容放在子组件的对应的位置，还要注意的是，如果用v-slot:title和#title的时候，在外层必须用template来套着，name='title'的话，好像就不需要套template，这是需
要注意的地方
2. sourceMap的作用，就是找到源代码和打包之后的代码的映射关系，以至于报错的时候，方便查找自己哪里错了，会显示在源代码，也就是自己写的代码中的错误位置
3. 用了postcss-px-to-viewport之后，内联样式是不生效的，好像暂时只看到了内联的样式是不会生效的，这个插件用于把px转换为视口的宽度值，在我的理解来说，比如给的原型图宽度是30px，然后通过插件转换
之后，加入就变成了4vw,然后在我们更改设备的时候，设备变了，宽度也变了，但是4vw还是4vw，这个是不会变的，只是实际所占的宽度改变了，因为现在的设备宽度变了，所以4vw就变成了此时设备的4vw,也就跟着
转换成了对应的px值，所以才实现了适配，这就是我的理解
4. vue的样式绑定用三元运算符很适合，能够减少大量的重复代码。印象最深刻的是单选框的使用，配合是否选中，决定想要的样式.
5. 很重要很重要很重要，今天学到的一招，以前都没注意过这个问题，就是报错，xxx is not a function 这种问题一般是调用的这个方法的对象出了问题，比如这个方法是给一个数字用的，但
是调用的时候没有注意，调方法的这个对象变了，变成了字符串，那么就会报这种错，所以一般在调用方法的时候，一般事先会判断一下对象是否存在或者类型，不然就会报这种错。
6. autoprefixer这个加浏览器前缀的插件，配置好了，npm run build的时候，出现了问题，结果是因为在配置浏览器的那里出了问题，还有就是vue脚手架建项目的时候，就已经安装
了autoprefixer这个的，只是没有启用，所以只需要在vue.config.js里面配置一下就行了
7. axios默认的content-type是application/json,network里面是这种形式：{  name:xxx, age:xxx }， 而application/x-www-form-urlencoded这种是formdata这种形式：name:xxx, age:xxx，
要看后端需要的是哪种，如果要formdata的形式传参，那就需要QS来系列化，否则就可以不用QS
8. 组件的sync用法，主要是为了使用者方便，比如在父组件中传了个值money到子组件，然后子组件又需要改money的值，我们就在子组件的触发父组件事件那里写成 this.$emit("update:money", xxx);
这样就可以修改父组件的money了，不用再写一个父组件的修改事件，触发那里是固定写法，如果要传的值，也是需要修改的值，在父组件中写成:money.sync="money"就可以了
9. 请求数据的处理问题，有时候请求回来的数据直接就可以用了，就不用修改，直接放到自己定义的变量里面就可以了，但是有的时候，返回的数据可能不是我们所需要的格式，所以这个时候就需要在返回的时候，
先循环处理一遍返回的数据，先修改一下，以便于使用，还有就是发送请求的时候，如果所发送的数据和我们data里面的数据格式有出入，那么我们不能直接使用data里面的数据，要看情况，有时候需要深拷贝一下，
再修改一下格式，然后再发送请求，这样就不会影响到我们data里面的数据，如果直接把data里面的数据修改了，有可能会引起页面渲然出问题，因为改动了data里面的数据，注意
10. 解token值的方法    decodeURIComponent(escape(window.atob('token'.split('.')[1])))
11. 处理发布动态时遇到的图片问题，上传的时候传的是attchId,然后下载下来是乱码，这个时候为了方便一点，直接在请求回来的数据遍历的时候就处理数据，直接在这个时候就把
返回来的图片进行处理，改成可以直接放在src里面的格式，这样，不管在哪里用，都不需要再重新处理一次图片，很多数据都是这样，如果在用的时候发现还要进行很多的处理操作，
这个时候就可以想想是否合适，是否在获取回来的时候，就怼数据进行处理。在后面引用的时候，就不会那么的麻烦
12. 路由的replace和push的区别就是会不会向 history 栈添加一个新的记录，简单来说就是，如果用的push，返回的时候，会返回到上一页，如果是replace的话，不会返回上一页，
而是会回到上一页的上一页，具体情况用的时候就知道了
13. foreach的遍历，是没有返回值的，所以用foreach的时候，都是新建的一个空数组，然后在遍历旧数组的时候，直接把新的值push到新的数组里面去，还要注意的一点就是，如果遍历
数据是一个对象，那么在遍历更改的时候就会改变每一项的数据，因为是复杂类型的数据，而如果是简单类型的数据，遍历的时候修改了数据，也不会改变原数组的，注意这一点
14. foreach遍历是不能用普通的方法来结束循环的，break是不行的，return false也是不行，这个只会终止符合条件的这一次循环，会继续之后的循环，就是说终止了当前的条件执行，
并没有终止整个循环的执行，要想终止循环，需要抛出异常的方式来终止执行
15. api封装的时候，尽量还是把参数一起放在api的文件夹里，不要放在组件发请求的地方，因为这个接口可能被不同的组件调用，如果写在组件里面，改的时候，需要改
多个组件，如果是放在api里，那么久只需要改api一个地方就可以了。所以尽量写在api文件里，还有就是比如要判断是否登录这种，因为用的地方可能很多，可能不同的场景
都需要判断是否登录了，这种也可以统一写一个方法，放utils里面，这样的话，就不需要在要判断状态的组件里都写方法，改起来也比较方便，

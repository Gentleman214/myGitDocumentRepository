## Vuex
以全局单例模式管理共享状态
***
五个部分，state，getters，mutations，actions，modules
#### 1.state
state是数据源，通过this.$store.state取到。
#### 2.getters
vuex中的的getter相当于vue中的computed计算属性，只有依赖项发生改变时才会重新计算。
getter也是取数据的，只不过可以在上面进行逻辑运算。
#### 3.mutations
mutations更改store中的状态，不可包含异步操作。
#### 4.actions
actions提交mutations，不直接变更状态，可以包含异步操作。
#### 5.modules
store又可以分模块（module），每个模块拥有自己的state，mutation，action，getter。


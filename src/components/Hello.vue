<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>

    <form>
      <input type="text" name="username"  placeholder="请输入用户名" v-model="userName"> <br>
      <input type="text" name="age" id="" placeholder="请输入用户年龄"  v-model="age"> <br>
      <a href="javascript:;" @click="addUser">提交</a>
    </form>
    
    <ul>
      <li v-for="article in articles"><a target="_blank" v-bind:href="article.alt">{{article.title}}</a></li>
    </ul>
    


  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      userName: '',
      age: '',
      articles: []
    }
  },
  beforeCreate (){
    console.log('beforeCreate');
  },
  created () {
    console.log('created');
  },
  beforeMount () {
    console.log('beforeMount');
  },
  mounted () {
    console.log('mounted');
    this.$http.jsonp('https://api.douban.com/v2/movie/top250?count=10', {}, {
          headers: {},
          emulateJSON: true
        }).then((response) => {
          // 这里是处理正确的回调

            this.articles = response.data.subjects
            // this.articles = response.data["subjects"] 也可以

        }, (response) => {
            // 这里是处理错误的回调
            console.log(response)
        })
  },
  methods: {
    addUser () {
      let name = this.userName
      let age = this.age
      this.$http.post('/api/user/addUser', {
        username: name,
        age: age
      }, {}).then((response) => {
        console.log(response)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

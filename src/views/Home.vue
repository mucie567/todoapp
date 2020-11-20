<template>
  <div class="home">
    <v-row class="home" justify="center">
      <div class="home-container">
        <h1>todos</h1>
        <v-card>
          <v-text-field
            v-model="newTitle"
            @keyup.enter="enterTask"
            placeholder="what needs to be done?"
            solo
            flat
            prepend-inner-icon="mdi-chevron-down"
            hide-details=""
            height="80"
          >

          </v-text-field>
          <div class="todo-list">
              <sample v-for="(todo,i) in todos" :key="i" :todo="todo"></sample>
              <!-- 앞의 todo props의 그리고 뒤의 todo는 vfor앞의 todo -->
          </div>
          <v-row class="todo-footer-extention" justify="center" align="center">
            <p style="position: absolute">{{todos.length}}items left</p>
            <v-btn text @click="filter='all'">All</v-btn>
            <v-btn text @click="filter='active'">Active</v-btn>
            <v-btn text @click="filter='completed'">Completed</v-btn>
          </v-row>
        </v-card>
      </div>
    </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
import { mapState } from "vuex";
export default {
  name: "Home",
  data(){
    return{
      newTitle:"",
      filter:"all"
    }
  },
  computed: {
    ...mapState(["todos"]),
    newTodoId(){
      return this.todos.reduce((acc,cur)=>{
        acc=Math.max(acc,cur.id)
        return acc
      },0)
    }
    //... es6문법
    // let dic1 ={'a':1,'b:':2}
    // undefined
    // dic1
    // {a: 1, b:: 2}
    // let dic2={'c':3,'d':4,dic1}
    // undefined
    // dic2
    // {c: 3, d: 4, dic1: {…}}
    // let dic2={'c':3,'d':4,...dic1}
    // undefined
    // dic2
    // {c: 3, d: 4, a: 1, b:: 2}
  },
  methods:{
    enterTask(){
      this.$store.commit('addTodo', {id:this.newId,title:this.newTitle,complete: false})
    }
  },
  components:{
    Sample: () => import("@/components/Sample.vue")
  }
};
</script>
<style lang="scss" scoped>
  .home{
    background: #f5f5f5;
  }
  .home-container{
    width: 1200px;
    min-width: 600px;
  }
  h1{
    color: #af2f2f26;
    font-size: 100px;
    font-weight: 400;
    text-align: center;
  }
  p{
    top: 10px;
    left: 10px;
  }
</style>

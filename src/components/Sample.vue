<template>
    <v-row no-gutters align="center" class="sample" @mouseover="mouseOver" @mouseleave="mouseLeave">
        <!-- <v-text-field solo
            flat
            hide-details=""
            height="80"
            clearable
        >

        </v-text-field> -->
        <div class="circle">
            <v-btn icon large color="green" @click="doComplete">
                <v-icon v-show="todo.complete">mdi-check</v-icon>
            </v-btn>
        </div>
        <p :class="{'complete-text': todo.complete}">{{todo.title}}</p>
        <v-spacer></v-spacer>
        <!-- 끝으로 보내는 방법 spacer -->
        <v-btn icon v-show="isMouseOver" ><v-icon>mdi-close</v-icon></v-btn>
    </v-row>
</template>

<script>
    export default {
        name:'Sample',
        props:["todo"],
        data() {
            return{
                isMouseOver: false,
                isComplete: this.todo.complete
            }
        },
        methods:{
            doComplete(){
                this.isComplete = !this.isComplete;
                this.$store.commit('editTodo', {
                    id:this.todo.id,
                    complete: this.isComplete,
                    title:this.todo.title
                });
            },
            mouseOver(){
                this.isMouseOver = true;
            },
            mouseLeave(){
                this.isMouseOver = false;
            }
        }
    }
</script>

<style lang="scss" scoped>
.sample{
    border-bottom: 1px solid #ededed;
    .circle{
        margin: 5px;
        
        width: 38px;
        height: 38px;
        border-radius: 25px;
        border: 1px solid gray;
    }
    p{
        margin: 0 10px;
        font-size: 25px;
    }
}
.complete-text{
    text-decoration: line-through;
}
</style>
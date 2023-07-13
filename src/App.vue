<template>
    <section class="to-do">
        <div class="to-do__container container">
            <h1 class="to-do__title">To Do List</h1>
            <div class="to-do__inner">
                <div class="to-do__inner-title">Add your personal tasks!</div>
                <div class="to-do__content">
                    <div class="to-do__addition">
                        <img class="to-do__addition-img" src="../public/img/todo.png" alt="">
                        <div class="to-do__addition-title">You can add task here</div>
                        <div class="to-do__form" id="form">
                            <input v-model="task" v-on:keydown.enter="add" v-on:input="changeInput" class="to-do__input" type="text" placeholder="Text Task" required="" id="taskInput">
                            <p v-if="hasTask" class="to-do__error">This task already exists</p>
                            <div class="to-do__form-bottom">
                                <button  @click="add" class="to-do__button" type="button" id="btn">Add task</button>
                                <div class="to-do__form-icons">
                                    <img src="../public/img/icons/1.svg" alt="" class="to-do__form-icon">
                                    <img src="../public/img/icons/2.svg" alt="" class="to-do__form-icon">
                                    <img src="../public/img/icons/3.svg" alt="" class="to-do__form-icon">
                                </div>
                            </div>
                          </div>
                    </div>
                    <div class="tasks">
                        <ul class="tasks__list" id="tasksList">
                            <li v-if="tasks.length === 0" class="tasks__item tasks__item--empty" id="emptyList">
                                <p class="task__item-title">Empty</p>
                                <img class="task__item-icon" src="../public/img/icons/icon-empty.svg" alt="" >
                            </li>
                            <li :key="t.name" 
                                v-for="t in tasks"
                                :class="{'tasks__item--done': t.isDone}"
                                class="tasks__item">
                                <p 
                                  :class="{'task__item-title--done': t.isDone}"
                                  class="task__item-title">{{t.name}}
                                </p>
                                <div class="task__buttons">
                                <button v-on:click="markAsDone(t)" class="task__button" type="button" data-type="done">
                                    <i class="fa-solid fa-check">&#10004;</i>
                                </button>
                                <button v-on:click="remove(t)" class="task__button" type="button" data-type="delete">
                                    <i class="fa-solid fa-xmark">&#10008;</i>
                                </button>
                              </div>
                            </li>
                
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      task: '',
      tasks: [],
    }
  },
  computed:{
    hasTask(){
      return this.tasks.find(t => this.task.toLowerCase() === t.name.toLowerCase() )
    }
  },

  methods:{
    add(){
      const newTask = {
        name: this.task,
        isDone: false
      }


      if (newTask.name.split(" ").join("") !== ''){
        if(!this.hasTask){
          this.tasks.push(newTask)
          this.task = ''
        }

      }


      
    },
    remove(task){
      this.tasks = this.tasks.filter(t => task.name !== t.name)
    },
    markAsDone(task) {
      task.isDone = !task.isDone;
    },
    changeInput(){

      if(this.tasks.find(t => this.task === t.name )){
          this.hasTask = true
        }
      else{
          this.hasTask = false
      }
    }
  }
}
</script>

<style src="../public/style.css"></style>

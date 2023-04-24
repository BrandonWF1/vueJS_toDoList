<template>
  <div class="container">
    <div class="content">
      <header class="header-block">
        <h1 class="header-block__title">Vue.ToDoList</h1>
      </header>
      <main>

        <section class="first-section">
          <div class="first-section__add-task">
          <popup-window :popup-opacity="popupOpacity" :popup-visible="popupVisible" @createPost="addNewTask" @closePop="closePopup" @openPop="openPopup"/>
          </div>
        </section>

        <section class="second-section">
          <task-item v-for="(task,index) of tasks" :task="task" :key="task.id" @completeTask="toggleComplete(index,task)" @deleteTask="deleteTask(index)"/>
        </section>

      </main>
    </div>
  </div>
</template>

<script>
import TaskItem from "@/components/TaskItem.vue";
import PopupWindow from "@/components/PopupWindow.vue";

export default {
    components: {
        PopupWindow,
      TaskItem
    },
    data() {
        return {
            tasks: [
                {
                    id: 1,
                    task: 'Изучить HTML+CSS',
                    complete: true,
                    date: '01.08.2021'
                },
                {
                    id: 2,
                    task: 'Изучить JavaScript',
                    complete: true,
                    date: '10.08.2021'
                },
                {
                    id: 3,
                    task: 'Написать свой первый проект на Vue.js',
                    complete: false,
                    date: '01.09.2021'
                },
                {
                    id: 4,
                    task: 'Сделать еще несколько проектов на Vue.js',
                    complete: false,
                    date: '01.12.2021'
                },
                {
                    id: 5,
                    task: 'Получить работу в IT-компании',
                    complete: false,
                    date: '01.12.2021'
                }
            ],
            popupVisible: 'none',
            popupOpacity: 0,
            newTaskText: '',
            newTaskDate: '',
        }
    },

    methods: {
        openPopup() {
            this.popupVisible = 'block'
            this.popupOpacity = 1
        },
        closePopup() {
            this.popupVisible = 'none'
            this.popupOpacity = 0
        },
        addNewTask(newTask) {
            this.tasks.push(newTask)
        },
        toggleComplete(index,task) {
          task.complete = !task.complete
        },
        deleteTask(index){
          this.tasks.splice(index,1)
        }
    }
}
</script>

<style lang="scss">

body {
  background: -webkit-linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  background: -moz-linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  background: linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  background-attachment: fixed;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Inter', sans-serif;
}

.content {
  width: 40%;
  background-color: white;
  border-radius: 50px;
  padding: 2rem;
}

.header-block {
  &__title {
    width: 100%;
    text-align: left;
    font-size: 2.5rem;
    font-weight: 700;
    padding: 0 2rem 0 2rem;
    color: transparent;
    -webkit-background-clip: text;
    background-clip: text;
    background-image: linear-gradient(135deg, rgb(204, 170, 247), rgb(14, 0, 141));
  }
}

.first-section {
  margin-bottom: 2rem;

  &__add-task {
    //display: flex; //на случай, если захочу кнопочку в центр
    //justify-content: center;
  }

  &__popup_window {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.8);
    display: none;
    opacity: 0; //не работает
    transition: opacity 0.8s ease-in-out; /* добавляем transition для свойства opacity */
    //не работает почему-то?
  }
}


.second-section {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: space-evenly;

  //класс для чекбокса, можно использовать вместо кнопок.
  &__checkbox {
    width: 20px;
    height: 20px;
    border: 1px solid #ccc;
    border-radius: 3px;
    background-color: #fff;

    &:checked {
      background-color: #007bff;
    }
  }
}




</style>
<template>
  <div v-bind:style="{ backgroundColor: task.complete ? '#7f71fe33' : 'white',transition: '400ms ease all' }"
       class="second-section__task task">
    <h2 class="second-section__task-date">{{ task.date }}</h2>
    <h2 class="second-section__task-name">{{ task.task }}</h2>
    <div class="second-section__completion-buttons">
      <button @click="deleteTask(index)" class="second-section__delete-btn">
        <img src="@/assets/close_icons.svg" alt="close-icon">
      </button>
      <button @click="toggleComplete(index,task)" class="second-section__unfinished-btn"
      v-bind:style="{ backgroundColor: task.complete ? '#007BFF7F' : '#ccaff7',transition: '400ms ease all'} ">
        {{ task.complete ? 'Отменить' : 'Завершить' }}
      </button>
<!--      <button class="second-section__finished-btn">-->
<!--      Завершить-->
<!--      </button>-->
<!--            <input class="second-section__checkbox" type="checkbox" v-model="task.complete">-->
    </div>


  </div>
</template>

<script>
import index from "vuex";

export default {
    props: {
        task: {
            type: Object,
            required: true,
        }
    },
    methods: {
        toggleComplete() {
            this.$emit('completeTask', null )
        },
        deleteTask(){
            this.$emit('deleteTask', null)
        }
    }
}
</script>

<style lang="scss" scoped>
.second-section {
  &__task {
    text-align: center;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    overflow: hidden;
    padding: 1rem;
    margin-bottom: 1rem;
    border: 1px solid rgba(1, 1, 1, 0.3);
    border-radius: 15px;
  }

  &__task-name {
    font-weight: 500;
    font-size: 1.2rem;
    width: 70%;
    overflow: hidden;

  }

  &__task-date {
    //width: 20%;
    font-size: 1.2rem;
    font-weight: 500;
    text-align: center;
    //margin:0 auto;
  }
  &__completion-buttons {
    position: relative;
    width: 15%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-right: 20px;
    button {
      padding:10px;
      font-size: 1rem;
      font-weight: 700;
      text-decoration: none;
      cursor: pointer;
      border: none;
      color: #fff;
      //background-color: #7f71fe;
      border-radius: 10px;
      transition: all 0.3s ease-in;
      &:hover{
        transform: scale(1.1);
        transition-duration: 300ms;
      }
    }

    img {
      width: 24px;
    }
  }
  &__delete-btn{
    position: absolute;
    background-color: rgba(0,0,0,0);
    //значнеия при двух кнопках
    //bottom: 55px;
    //left: 100px;
    bottom: 20px;
    left: 100px;
    &:hover{
      scale: 1.5;
    }
  }
  &__unfinished-btn{
    //margin-bottom: 10px; // при двух кнопках
    background-color: rgba(0, 123, 255, 0.5);

  }
  &__finished-btn{
    background-color: #ccaff7;
  }

}
</style>
<template>
  <div v-bind:style="{ backgroundColor: task.complete ? '#7f71fe33' : 'white',transition: '400ms ease all' }"
       class="second-section__task task">
    <h2 class="second-section__task-date">{{ task.date }}</h2>
    <h2 class="second-section__task-name">{{ task.task }}</h2>
    <div class="second-section__completion-buttons">
<!--      <button class="second-section__delete-btn">-->
<!--        <img src="@/assets/close_icons.svg" alt="close-icon">-->
<!--      </button>-->
<!--      <button class="second-section__unfinished-btn">-->
<!--        Отменить-->
<!--      </button>-->
<!--      <button class="second-section__finished-btn">-->
<!--      Завершить-->
<!--      </button>-->
            <input class="second-section__checkbox" type="checkbox" v-model="task.complete">
    </div>


  </div>
</template>

<script>
export default {
    props: {
        task: {
            type: Object,
            required: true,
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
      width: 1.4rem;
    }
  }
  &__delete-btn{
    position: absolute;
    background-color: rgba(0,0,0,0);
    bottom: 55px;
    left: 100px;
    &:hover{
      scale: 1.5;
    }
  }
  &__unfinished-btn{
    margin-bottom: 10px;
    background-color: rgba(0, 123, 255, 0.5);

  }
  &__finished-btn{
    background-color: #ccaff7;
  }

}
</style>
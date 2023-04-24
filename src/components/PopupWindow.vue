<template>
  <button class="first-section__popup_href" @click="openPopup">Новое задание</button>
  <div class="first-section__popup_window"
       :style="{display: popupVisible,opacity: popupOpacity, transition: 'opacity 0.5s ease-in-out all'}">
    <form @submit.prevent>

      <div class="popup">

        <button class="close-popup"><img src="@/assets/close_icons.svg" alt="close-icon" @click="closePopup">
        </button>

        <input class="popup__input-text popup_item" type="text" v-model="newTaskText">
        <input class="popup__input-text popup_item" type="date" v-model="newTaskDate">
        <button class="popup__add-btn popup_item" @click="addNewTask">Добавить</button>


      </div>
    </form>
  </div>
</template>

<script>
export default {
    props: {
        popupVisible: {
            type: String,
            required: true
        },
        popupOpacity: {
            type: Number,
            required: true
        }
    },
    data() {
      return{
          newTaskText: '',
          newTaskDate: '',
      }
    },
    methods:{
        closePopup() {
            this.$emit('closePop', null)
        },
        openPopup() {
            this.$emit('openPop', null)
        },
        addNewTask() {
            let inputDate = new Date(this.newTaskDate); // преобразуем введенную дату в объект Date
            let day = inputDate.getDate().toString().padStart(2, '0'); // получаем день месяца как строку и дополняем его 0 при необходимости
            let month = (inputDate.getMonth() + 1).toString().padStart(2, '0'); // получаем месяц (начиная с 0) и дополняем его 0 при необходимости
            let year = inputDate.getFullYear().toString(); // получаем год как строку
            let formattedDate = `${day}.${month}.${year}`; // создаем строку в нужном формате
            // ДОПИЛИТЬ ПРОВЕРКУ НА ВВОД ПОЛЬЗОВАТЕЛЯ, ЕСЛИ НИЧЕГО НЕ ВВЕДЕНО НЕ ВЫВОДИТЬ ЭЛЕМЕНТ ВОВСЕ
            const newTask = {
                id: Date.now(),
                task: this.newTaskText,
                complete: false,
                date: formattedDate
            }
            // this.tasks.push(newTask)
            this.$emit('createPost', newTask) //передается название и объект (аналог EventListener)
        }


    }
}
</script>

<style lang="scss" scoped>

.first-section {

  &__popup_href{
    position: relative;
    font-size: 1.5rem;
    text-align: center;
    display: inline-block;
    text-decoration: none;
    cursor: pointer;
    border: none;
    letter-spacing: 1px;
    height: 80px;
    width: 50%;
    padding: 0 30px;
    font-weight: 700;
    color: #fff;
    background-color: #7f71fe;
    border-radius: 10px;
    transition: all 0.3s ease-in;

    &:hover {
      background-color: rgb(204, 170, 247);
      transition: 500ms ease all;
    }
  }
  &__popup_window {
    position: fixed;
    width: 100%;
    z-index: 9999;
    height: 100%;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.8);
    display: none;
    opacity: 0;
    transition: opacity 0.8s ease-in-out;
  }

}
.popup {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  top: 50%;
  left: 50%;
  width: 800px;
  background: linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  padding: 60px 20px 20px 20px;
  transform: translate(-50%, -50%);
  border-radius: 30px;

  &_item {
    padding: 2rem;
    margin: 30px; //тупой костыль, ПЕРЕДЕЛАТЬ.
  }

  & .close-popup {
    position: absolute;
    top: 25px;
    right: 40px;
    cursor: pointer;
    border-radius: 100px;
    background-color: rgba(255, 255, 255, 0); //тупой костыль, потом подумаю как переделать
    border: none;
    transition: all 0.3s ease-in; // чтобы обратно тоже красиво выезжал))
    &:hover {
      background-color: #ccaff7;
      transition: all 500ms ease;
    }
  }

  &__input-text {
    border: 1px solid rgba(1, 1, 1, 0.3);
    border-radius: 10px;
    font-size: 2rem;

    &:focus {
      outline: none; /* отключаем обводку по умолчанию */
      transition: all 300ms ease;
      background-color: #ebdbff;
    }

    &:hover {
      transition: all 300ms ease;
      background-color: #ebdbff;
    }
  }

  &__add-btn {
    position: relative;
    font-size: 1.5rem;
    text-align: center;
    margin: 30px auto;
    text-decoration: none;
    cursor: pointer;
    border: none;
    letter-spacing: 1px;
    height: 80px;
    width: 50%;
    padding: 0 30px;
    font-weight: 700;
    color: #333;
    background-color: #fff;
    border-radius: 10px;
    transition: all 0.3s ease-in;

    &:hover {
      background-color: #ebdbff;
      transition: 500ms ease all;
    }
  }
}



</style>
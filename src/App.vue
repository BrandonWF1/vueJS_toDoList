<template>
  <div class="container">
    <div class="content">
      <header class="header-block">
        <h1 class="header-block__title">Vue.ToDoList</h1>
      </header>
      <main>
        <section class="first-section">
          <div class="first-section__add-task">
            <button class="first-section__popup_href open-popup" @click="openPopup">Новое задание</button>
            <!--            не работает фишка с popupOpacity, починить! Модальное окно не плавно появляется-->
            <div class="first-section__popup_window"
                 :style="{display: popupVisible,opacity: popupOpacity, transition: 'opacity 0.5s ease-in-out all'}">
              <form @submit.prevent>
                <!--                сначала я пытался сделать через @submit.prevent="addNewTask", но кнопка закрытия ломала мне весь алгоритм,разобраться-->
                <div class="popup">

                  <button class="close-popup"><img src="@/assets/close_icons.svg" alt="close-icon" @click="closePopup">
                  </button>
                  <input class="popup__input-text popup_item" type="text" v-model="newTaskText">
                  <input class="popup__input-text popup_item" type="date" v-model="newTaskDate">
                  <button class="popup__add-btn popup_item" @click="addNewTask">Добавить</button>
                  <!--                type="submit" -->

                </div>
              </form>
            </div>
            <!--        <input type="text" class="first-section__add-task-input">-->
            <!--        <button class="first-section__add-task-btn"></button>-->
          </div>

        </section>
        <section class="second-section">
          <div v-bind:style="{ backgroundColor: task.complete ? '#7f71fe33' : 'white',transition: '400ms ease all' }"
               v-for="task of tasks" class="second-section__task task">
            <h2 class="second-section__task-date">{{ task.date }}</h2>
            <h2 class="second-section__task-name">{{ task.task }}</h2>
            <div class="second-section__completion-buttons">
              <!--              <button class="second-section__unfinished-btn"><img src="@/assets/cancel_icons.svg" alt="cancel_btn">-->
              <!--              </button>-->
              <!--              <button class="second-section__finished-btn"><img src="@/assets/check_icons.svg" alt="check_btn"></button>-->
              <input class="second-section__checkbox" type="checkbox" v-model="task.complete">

            </div>


          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
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
        addNewTask() {
            let inputDate = new Date(this.newTaskDate); // преобразуем введенную дату в объект Date
            let day = inputDate.getDate().toString().padStart(2, '0'); // получаем день месяца как строку и дополняем его 0 при необходимости
            let month = (inputDate.getMonth() + 1).toString().padStart(2, '0'); // получаем месяц (начиная с 0) и дополняем его 0 при необходимости
            let year = inputDate.getFullYear().toString(); // получаем год как строку
            let formattedDate = `${day}.${month}.${year}`; // создаем строку в нужном формате
            // ДОПИЛИТЬ ПРОВЕРКУ НА ВВОД ПОЛЬЗОВАТЕЛЯ, ЕСЛИ НИЧЕГО НЕ ВВЕДЕНО НЕ ВЫВОДИТЬ ЭЛЕМЕНТ ВОВСЕ
            const newTask = {
                id: this.tasks.length + 1,
                task: this.newTaskText,
                complete: false,
                date: formattedDate
            }
            this.tasks.push(newTask)
        }
    }

}
</script>

<style lang="scss">
body {
  background: -webkit-linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  background: -moz-linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  background: linear-gradient(135deg, rgb(204, 170, 247) 3%, rgb(65, 52, 187));
  //background-size: cover;
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
    //color: transparent;
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

  &__popup_href {
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
      //background: linear-gradient(0deg, rgb(204, 170, 247), rgb(65, 52, 187)); //здесь не работает transition, хотя для Close popup работает, чзХ?? Возможно дело в градиенте
      background-color: rgb(204, 170, 247); //тут работает
      transition: 500ms ease all;
    }
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

  &__task-name {
    font-weight: 500;
    font-size: 1.2rem;
  }

  &__completion-buttons {
    width: 15%;
    display: flex;
    justify-content: center;
    align-items: center;

    button {
      text-decoration: none;
      cursor: pointer;
      border: none;
      color: #fff;
      background-color: #7f71fe;
      border-radius: 10px;
      transition: all 0.3s ease-in;
    }

    img {
      width: 2.5rem;
    }
  }

  &__checkbox {
    width: 20px;
    height: 20px;
    border: 1px solid #ccc; // СТИЛИ ЧЕКБОКСА НЕ СРАЗУ ПРОГРУЖАЮТСЯ, А СПУСТЯ 5 МИНУТ РАБОТЫ НА САЙТЕ. ПОЧИНИТЬ.
    border-radius: 3px;
    background-color: #fff;

    &:checked {
      background-color: #007bff; //то работает, то не работает, надо починить и понять почему не сразу срабатывает
    }
  }

  &__task-date {
    //width: 20%;
    font-size: 1.2rem;
    font-weight: 500;
    text-align: center;
    //margin:0 auto;
  }

  &__task-name {
    width: 70%;
    //margin: 0 auto;
    overflow: hidden;
  }
}

// ===============================================================

//отдельные классы вне какой-либо  section

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
  &__add-btn{
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


.task {
  text-align: center;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  overflow: hidden;
  padding: 1rem;
  margin-bottom: 1rem;
  border: 1px solid rgba(1, 1, 1, 0.3);
  border-radius: 15px;
}




</style>
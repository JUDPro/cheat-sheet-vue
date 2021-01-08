<template>
  <div id="app">
    <div class="test">
      <div class="text">Обучалка-шпаргалка</div>
      <div class="block">
        <!--Декларативная отрисовка-->
        <p>Декларативная отрисовка</p>
        <div class="text-small" :title="someTitle">{{someText}}</div>
        <!--Условия и циклы-->
        <p>Условия и циклы</p>
        <div class="text-small" v-if="seen">
          Текст, который можно скрывать/показывать.
        </div>
        <button @click="seen = !seen">
          Нажми, чтобы скрыть/показать.
        </button>
        <div class="text-small"><h4>Здесь цикл v-for:</h4>
          <input type="text" v-model="containerNewElement">
          <button @click.prevent="addNewElement()">
            Нажми, чтобы добавить элемент массива.
          </button>
          <div class="text-small" v-for="m in array" :key="m.id">
            {{m.item}}
          </div>
        </div>
        <!--Компонент-->
        <p>Компонент</p>
        <someComponent :someProps="'Передаю что-то в компонент'"></someComponent>
        <someComponent v-for="el in someValue" :someProps="el" :key="el.id"></someComponent>
        <!--Хуки жизненного цикла-->
        <p>Хуки жизненного цикла</p>
        <button @click="seenHooksComponent = !seenHooksComponent">
          Скрываю компоненту/показываю компоненту
        </button>
        <lifeHooks v-if="seenHooksComponent"></lifeHooks>
        <!--Вычисляемые свойства-->
        <p>Вычисляемые свойства</p>
        <div class="block">
          <div><b>Сообщение: </b>"{{myMes}}"</div>
          <div><b>То же сообщение, только перевернутое:</b> "{{reverseMes}}"</div>
        </div>
        <div class="block">
          <input type="text" v-model="newName">
          <button @click.prevent="addNewName()">Нажмите, чтобы дать новое имя!</button>
          <div>{{firstName}} {{lastName}}</div>
          <div>{{fullName}}</div>
        </div>
        <!--Методы-наблюдатели-->
        <p>Методы-наблюдатели</p>
      </div>
    </div>
  </div>
</template>

<script>
import someComponent from './components/someComponent.vue';
import lifeHooks from './components/testlifehooks.vue';

export default {
  name: 'app',
  components: {
    someComponent,
    lifeHooks,
  },
  data: () => ({
    someText: 'Наведи на этот текст курсором.',
    someTitle: 'Некоторое сообщение',
    seen: true,
    containerNewElement: '',
    array: [
      { item: 'Первый элемент массива' },
      { item: 'Второй элемент массива' },
      { item: 'Третий элемент массива' },
    ],
    someValue: [
      { id: 0, item: 1 },
      { id: 1, item: 2 },
      { id: 2, item: 3 },
    ],
    seenHooksComponent: true,
    myMes: 'Для меня это послужит шпаргалкой',
    firstName: 'Иван',
    lastName: 'Иванов',
    newName: '',
  }),
  computed: {
    reverseMes() {
      return this.myMes.split('').reverse().join('');
    },
    fullName: {
      get() {
        return (this.firstName, ' ', this.lastName);
      },
      set(newValue) {
        const names = newValue.split(' ');
        [this.firstName] = names; //  здесь деструкция массива. Было this.firstName = names[0]
        this.lastName = names[names.length - 1];
      },
    },
  },
  methods: {
    addNewElement() {
      // const i = this.containerNewElement;
      // this.array.push(i);
      this.$set(this.array, this.array.length, {
        item: (this.containerNewElement), // добавил работующий метод
      });
    },
    addNewName() {
      this.fullName = this.newName;
    },
  },
  /* Хуки жц */
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeDestroy() {},
  destroyed() {},
  /* Хуки жц */
};
</script>

<style>
#app {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.test {
  width: 80%;
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.text {
  font-size: 40px;
  font-weight: 600;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 1px solid black;
}

.text-small {
  font-size: 18px;
  padding: 5px;
  border: 1px solid gray;
  margin: 10px;
}

p {
  font-size: 25px;
  font-weight: 400;
  padding: 10px;
  border-bottom: 1px solid black;
  background-color: #bdbdbd;
}

button {
  height: 30px;
  margin: 3px;
  font-size: 15px;
}

input {
  height: 24px;
  font-size: 15px;
}

.block {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
}
</style>

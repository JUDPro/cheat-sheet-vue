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
          <button @click="addNewElement()">
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
          Убираю компоненту/создаю компоненту
        </button>
        <lifeHooks v-if="seenHooksComponent"></lifeHooks>
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
  }),
  methods: {
    addNewElement() {
      const i = this.containerNewElement;
      this.array.push(i);
    },
  },
  /* Хуки жц */
  beforeCreate: {},
  created: {},
  beforeMount: {},
  mounted: {},
  beforeUpdate: {},
  updated: {},
  beforeDestroy: {},
  destroyed: {},
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
}
</style>

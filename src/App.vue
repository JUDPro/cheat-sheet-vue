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
        <s>что-то про наблюдателей</s>
        <!--Работа с классами и стилями-->
        <p>Связывание CSS-классов</p>
        <div class="static" :class="classObject">
          Некоторый текст для теста
          <button @click="isActive = !isActive">
            меняю стили
          </button>
          <button @click="error = 'fatal'">
            вызываю ошибку
          </button>
        </div>
        <!--
          В примере с массивом, берется его последний элемент по дефолту,
          соответственно и класс этого элемента
        -->
        <div class="static" :class="[ activeClass, errorClass ]">
          Пример с массивом
        </div>
        <!--
          Можно использовать тернарные условия
        -->
        <div class="static" :class="[isActive ? activeClass : '', errorClass]">
          Массив с условием
        </div>
        <div class="static" :class="[{ active: isActive }, errorClass]">
          Пример с массивом и объектом
        </div>
        <div class="block">
          С использованием компонентов
          <cssComponent :class="classObject"></cssComponent>
          <button @click="isActive = !isActive">
            меняю стили
          </button>
        </div>
        <!--Связывние inline-стилей-->
        <p>Связывние inline-стилей</p>
        <div class="block">Использование объектов:
          <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">Пример</div>
          <!--Пример с объектом в data делает код чище-->
          <div :style="styleObject">Пример с объектом в data</div>
          <div :style="[baseStyles, overridingStyles]">Пример с массивом</div>
        </div>
        <div class="block">
          При использовании в v-bind:style свойств CSS,<br/>
          требующих указания вендорных префиксов,<br/>
          Vue автоматически определит это и добавит<br/>
          подходящие префиксы к применяемым стилям.
        </div>
        <div v-bind:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }">
          Здесь флексы будут отображаться в браузерах, где они не поддерживаются
        </div>
        <!--условная отрисовка-->
        <p>Условная отрисовка</p>
        <div class="block">
          <button @click="awesome = !awesome">Отрисовка разных элементов</button>
          <div class="examp1" v-if="awesome">
            <div>awesome: true</div>
          </div>
          <div class="examp2" v-else>
            <div>awesome: false</div>
          </div>
        </div>
        <div class="block">
          Управление повторным использованием элементов при помощи key:
          <div class="auth" v-if="loginType">
            Введите email: <input type="text" placeholder="Введите email" key="username-input">
          </div>
          <div class="auth" v-else>
            Введите логин: <input type="text" placeholder="Введите логин" key="email-input">
          </div>
          <button @click="loginType = !loginType">Поменять тип входа</button>
        </div>
        <!--Отрисовка списков-->
        <p>Отрисовка списков</p>
        <div class="block">
          <ul>
            <li v-for="item in items" :key="item.message">
              {{ item.message }}
            </li>
          </ul>
          <!--Ниже пример с индексом, думаю, поможет в будущем-->
          <ul>
            <li v-for="(item, index) in items" :key="item.message">
              {{ index }} - {{ item.message }}
            </li>
          </ul>
          <!--Можно итерировать объект-->
          <div class="block">Здесь в v-for прогоняю объект: </div>
          <u>
            <li v-for="value in object" :key="value.id">
              {{ value }}
            </li>
          </u>
          <!--Можно итерировать объект со свойством-->
          <div class="block">Здесь в v-for прогоняю объект со свойством: </div>
          <u>
            <li v-for="(index, value, name) in object" :key="value.id">
              {{ index }}. {{ name }}: {{ value }}
            </li>
          </u>
        </div>
        <!--Отслеживание изменений в массиве-->
        <p>Отслеживание изменений в массиве</p>
        <div class="btnTest">
          <div class="block">
            #Методы внесения изменений в массив:
            <input type="text" v-model="testValueForArray">
            <!--Добавляет в массив новый элемент-->
            <button @click="myArray.push({ elem: testValueForArray })">push</button>
            <!--Удаляет последний элемент в массиве-->
            <button @click="myArray.pop()">pop</button>
            <!--Удаляет первый элемент в массиве-->
            <button @click="myArray.shift()">shift</button>
            <!--Добавляет новый элемент в начало массива-->
            <button @click="myArray.unshift({ elem: testValueForArray })">unshift</button>
            <input type="text" v-model="valueForTest">
            <!--
              Удаляет нужный элемент, 1 параметр - какой элемент нужен,
              второй параметр - сколько удалить
            -->
            <button @click="myArray.splice( valueForTest, 1 )">splice</button>
            <!--
              А этот пример интересный, с помощью этого примера можно и
              удалять элементы, и добавлять, и заменять!
            -->
            <button @click="myArray.splice( valueForTest, 1, { elem: testValueForArray })">
              splice со вставкой
            </button>
            <button @click="myArray.sort()">sort</button>
            <button @click="myArray.reverse()">reverse</button>
          </div>
          <div class="block">
            <ul>
              <li v-for="(i, index) in myArray" :key="i.elem">
                {{ index }}. {{ i.elem }}
              </li>
            </ul>
          </div>
        </div>
        <div class="block">
            #Замены в массиве:
            <!--
              С помощью метода slice() можно возвращать новый массив,
              используя данные существующего.
              Если в аргументах указать цифру, то вернется массив начиная
              с той цифры, которую я указал (то есть со второго элемента,
              в данном примере).
              Если указать два аргумента (укащать две цифры),
              то вернется массив с N элемента по M элемент.
            -->
            <button @click="someArray = myArray.slice(2)">slice</button>
            <!--
              Метод concat возвращает массив, объединенный из двух.
              см пример.
              p.s. Данный пример не очень хороший, тк вызывает ошибку <(Т_Т)>
              Duplicate keys detected
            -->
            <button @click="someArray = myArray.concat(someArray)">concat</button>
            <!--
              Из названия понятно для чего этот метод. На вход кушоет функцию.
              Нужно вернуться потом к этому методу ((((((((((((
            -->
            <button
              @click="someArray = numberArray.filter(testFilterFun(3, 6))">
              filter
            </button>
            <ul>
              <li v-for="item in someArray" :key="item.elem">
                {{item.elem}}
              </li>
            </ul>
        </div>
        <div class="block">
          Фильтрация и отображение массива с вычисляемым свойством:
          <li v-for="n in evenString" :key="n.id">{{ n }}</li>
          когда вычисляемые свойства невозможно использовать:
          <!--ul v-for="set in sets" :key="set.id">
            <li v-for="n in even(set)" :key="n.id">{{ n }}</li>
          </ul-->
          <div>а вот фиг знает, пример из доки вью не робит</div>
        </div>
        <div class="block">
          #v-for диапазоны:
          <!--В v-for можно передать целое число-->
          <div>
            <span v-for="n in 10" :key="n.id">{{ n }}</span>
          </div>
        </div>
        <p>Обработка событий</p>
        <div class="block">
          <button @click="counter += 1">+1</button>
          <div>{{ counter }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import someComponent from './components/someComponent.vue';
import lifeHooks from './components/testlifehooks.vue';
import cssComponent from './components/testCssComponent.vue';

export default {
  name: 'app',
  components: {
    someComponent,
    lifeHooks,
    cssComponent,
  },
  data: () => ({
    counter: 0,
    sets: [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]],
    numberArray: [1, 2, 3, 4, 5, 6, 7, 8, 9],
    someArray: [],
    valueForTest: 0,
    testValueForArray: '',
    myArray: [
      { elem: 'first element' },
      { elem: 'second element' },
      { elem: 'threeth element' },
      { elem: 'fourth element' },
      { elem: 'fifth element' },
    ],
    object: {
      one: 'Тест',
      two: 'Test',
      param: 3,
    },
    items: [
      { message: 'one' },
      { message: 'two' },
      { message: 'foo' },
      { message: 'bar' },
      { message: 'baz' },
      { message: 'test' },
      { message: 'зачем я это писал?._.' },
    ],
    loginType: 'username',
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
    //  classObject: {
    //  isActive: true,
    //  hasError: false,
    //  },
    isActive: true,
    hasError: false,
    error: null,
    activeClass: 'active',
    errorClass: 'text-danger',
    activeColor: 'red',
    fontSize: 30,
    styleObject: {
      color: 'blue',
      fontSize: '25px',
    },
    baseStyles: {
      color: 'orange',
      fontSize: '25px',
    },
    overridingStyles: {
      color: 'red',
      fontSize: '30px',
    },
    awesome: true,
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
    classObject() {
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error === 'fatal',
      };
    },
    evenString() {
      return this.numberArray.filter(
        // eslint-disable-next-line
        function (number) {
          return number % 2 && number < 9;
        },
      );
    },
    even(numbers) {
      return numbers.filter(
      // eslint-disable-next-line
        function (number) {
          return number % 2 === 0;
        },
      );
    },
  },
  methods: {
    sortArray(a, b) {
      if (a > b) return 1;
      if (a === b) return 0;
      if (a < b) return -1;
      return null;
    }, // до сих пор не понял, как должен работать sort() метод. Да и eslint все ломает
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
    testFilterFun(a, b) {
      // eslint-disable-next-line
      return function (x) {
        return x >= a && x <= b;
      };
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

.static {
  color: darkblue;
  background-color: burlywood;
  padding: 15px;
  margin: 5px;
}

.active {
  background-color: black;
  color: white;
}

.text-danger {
  background-color: red;
  color: white;
}

.examp1 {
  width: 100px;
  height: 150px;
  background-color: brown;
  margin: 15px;
  color: white;
  display: flex;
  align-items: center;
  text-align: center;
}

.examp2 {
  width: 150px;
  height: 100px;
  background-color: chocolate;
  margin: 15px;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
}

.auth {
  margin: 15px;
}

.btnTest{
  display: flex;
  padding: 15px;
}
</style>

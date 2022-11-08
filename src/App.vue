<template>
  <h1>Vue 3 入門</h1>
  <p>{{ message1 }}</p>

  <p v-text="message2"></p>

  <p v-html="htmlmessage"></p>

  <div>
    <a v-bind:href="link" v-text="message41"></a><br/>
    <a href=":link" v-text="message42"></a>
  </div>

  <div>
    <!-- オブジェクトのプロパティにfalseやtrueを指定することで
        class="active"を適用できるか決める。
        適用したいクラス名を''で囲うと、複数のクラスを同時に指定できる。
        {}の中を,で区切ると、複数の変数に応じたクラスの適用を実現できる。
     -->
    <p v-bind:class="{'active under_line5': isActive5, blue5: isBlueActive5}" v-text="message5"></p>
    <!-- 同時に普通にクラスを指定することもできる -->
    <p :class="{active: isActive5}" class="under_line5" v-text="message5"></p>
    <!-- 三項演算子（や論理演算子|| &&）も利用できる  -->
    <p :class="isActive5 ? 'active' : 'blue5'" v-text="message5"></p>
    <p :class="[isActive5, isBlueActive5]" v-text="message5"></p>
  </div>
  <!-- styleを設定 -->
  <p :style="styleObject" v-text="message6"></p>

  <!-- v-if, v-else-if, v-else
   ↑は<template>タグの中でのみ使用。<script>タグの中では、普通にjsのif,else-if,else構文を使用する
   ブロック・要素単位で表示非表示・表示内容を切り替えることができる
   <div v-if="条件式">内容</div>
   errorが入っている時だけ表示 -->
  <div v-if="error">7. {{ error }}</div>
  <div v-if="stock">7. まだ商品の在庫数に余裕がございます。（{{ stock }}）</div>
  <div v-else-if="stock === 0">7. 申し訳ございません。売り切れです。（{{ stock }}）</div>
  <div v-else>7. 在庫数が少なくなっています。おいsぎください。（{{ stock }}）</div>

  <!-- v-show
  v-ifなどとは少し違い、true or false で表示っ非表示を切り替える。
  v-ifはfalseの時、要素自体が無くなるのに対し
  v-showは、要素自体は存在するがdisplay:noneで隠される
  v-showの方が処理が軽い-->
  <div v-show="error8">8. エラーが発生しています</div>

  <!-- v-for
  配列から要素を一つずつ取り出して表示できる
  jsのmapや、phpのforeachに似てる。

  v-forを使うときは、v-bindでkey属性に一意の値を設定する（Reactでもそうだった）
  -->
  <div v-for="language in languages9" :key="language">
    8. {{ language }}
  </div>
  <!-- indexを取得すると、現在何番目の要素なのかを確認できる -->
  <div v-for="(user, index) in user9" v-bind:key="user">
    9. {{index}}--{{ user.id}} : {{ user.name }} : {{ user.email }} : {{ user.admin }}
  </div>
  <p>9. 配列にv-forをし、取り出したオブジェクトにさらにv-forをして値を取り出す。</p>
  <div v-for="(user, index) in user9" :key="user">
    {{ index }}
    <span v-for="value in user" :key="value">
        {{ name }} : {{ value }}
      </span>
  </div>
  <p>9. v-ifで条件分岐して、admin以外は表示しない。</p>
  <div v-for="(user, index) in user9" :key="user">
    <div v-if="user.admin === true">
      {{ index }}
      <span v-for="value in user" :key="value">
          : {{ value }}
        </span>
    </div>
  </div>



  <!-- v-on:click
   v-onディレクティブを使うと、ユーザーの操作に応じたイベントを設定できる
   <div v-on:click="関数名"></div>
   ↑クリックされると関数が実行される

   @click（省略記法）、そのほかに、@dbclick（ダブルクリックで発火）、@submit、mouseoverなど色々ある。
   -->
  <div v-on:click="PlussButton"><button>+</button></div>
  <div v-text="number10"></div>
  <div @click="MinusButton"><button>-</button></div>

  <!-- event
   event.イベント修飾子（今回はリロードを防ぐpreventDefault()を使ってみた
   修飾子にもいろんな種類がある
   -->
  <button @click="clickButton11"><button>クリック11</button></button>
  <form @submit="send">
    <button>送信11</button>
  </form>
  <!-- scriptにeventを渡さなくても、これだけでも済む -->
  <form @submit.prevent="send">
    <button>送信11</button>
  </form>



  <!-- reactivity ref関数 -->
  <button type="button" @click="Count12" >12count is : {{ count }}</button>
  <button type="button" @click="Text12" >12text is : {{ message12 }}</button>

  <br>
  <!-- reactivity reactive関数
  v-modelを使用している場合は、valueは使えない-->
  <button type="button" @click="Button13">
    13. count is : {{ state13.count }}
  </button>



  <!-- v-model
   v-modelを使用している場合は、valueは使えない-->
  <p>14. ref関数とv-model</p>
  <p> {{ message14 }}</p>
  <input v-model="message14"/>
  <input :value="message14" @input="message14 = $event.target.value" />
  <div><button @click="clickButton14">Click</button></div>


  <p>15. reactive関数とv-model</p>
  <p>{{ message15.name }}</p>
  <input v-model="message15.name"/><br>
  <!-- v-model.lazy input要素からカーソルを外した際に変更を反映 -->
  <input v-model.lazy="message15.name"/><br>
  <!-- v-model.trim 入力地の先頭・最後に空白がある場合に自動で取り除く -->
  <input v-model.trim="message15.name"/><br>
  <!-- v-model.number type=textの時、入力値を文字列から数値に変換してくれる -->
  <input v-model.number="message_num15.text" type="text"/><br>
  <button @click="clickButton15">Click</button>


  <!-- computed -->
  <h2>16. fullname: {{ user16.firstName }} {{ user16.lastName }}</h2>
  <h2>fullname: {{ fullName16 }}</h2>

  <h3>17. fullname: {{ user17.firstName}} {{ user17.lastName}}</h3>
  <button @click="changeName17">Change Name</button>



  <!-- watcher + ref -->
  <button @click="count18++">Count : {{ count18 }}</button>



  <!-- watcher + reactive -->
  <button @click="state19.count++">Count: {{ state19.count }}</button>

</template>



<script setup>
import { ref, watch } from 'vue';
import { reactive, computed } from 'vue';

//19 watcher + reactive
const state19 = reactive({
  count: 0,
})
//第一引数に直接state19.countだけを指定しちゃだめ
//;
watch(() => state19.count, (count, previousCount) => {
  console.log('count:', count);
  console.log('previousCount:', previousCount);
});





//18 watcher + ref
const count18 = ref(0);
//第一引数に監視対象、第二引数の第一引数に変更後の値、第二引数に変更前の値が入る
watch(count18, (count, previousCount) => {
  console.log('count:', count);
  console.log('previousCount:', previousCount);
})


  //16 computed
  const user16 = reactive({
    firstName: 'John',
    lastName: 'Doe',
  })
  const fullName16 = computed(() => {
    return user16.firstName + user16.lastName;
  });
  //ちなみに関数でも同じようなことはできる
  const fullName = () => {
    return user16.firstName + user16.lastName;
  }
  //関数とcomputedの違いは、キャッシュ機能とゲッター・セッター
  //computedの値は、reactiveな変数の更新を反映する時にだけ再実行される。

  //computed setter
  //computedの値は直接は更新できない（fullName.value = '変更値' ❌）
  const user17 = reactive({
    firstName: 'fadfa',
    lastName: 'dfafa',
  })
  const fullName17 = computed({
    get(){
      return `${user17.firstName} ${user.lastName}`;
    },
    set(newValue) {
      const names = newValue.split(' ');
      user17.firstName = names[0];
      user17.lastName = names[names.length -1];
    }
  })
  const changeName17 = () => {
    fullName17.value = 'Jane Doe';
  };




  //15. v-model reactive
  const message15 = reactive({
    name : "sato takeru",
  });
  const message_num15 = reactive( {
    text : "1",
  });
  const clickButton15 = () => {
    console.log(typeof message_num15.text);
  }

  //14. v-model ref
  const message14 = ref('Hello, World');
  const clickButton14 = () => {
    console.log(message14.value);
  }




  //13. reactive関数
  //引数にはオブジェクト飲みを取る
  const state13 = reactive( {
    count: 0,
  })
  const Button13 = () => {
    state13.count ++;
  }



//12. ref関数
 //引数にはboolean, string, オブジェクトをとる
 const count = ref(0);
 //ref関数の場合、scriptタグ内でcountを直接更新することができない
 //count.valueを使うとできる
 const Count12 = () => {
   count.value ++;
   //count ++; これはだめ
 }
 const message12 = ref('武田');
 const Text12 = () => {
   message12.value = message12.value + "です";
  }




  //v-text
  let message1 = '1. Hello World';

  //関数の実行
  let message2 = '2. Hello World';
  const upperCase = () => {
    message2 = message2.toUpperCase();
  }
  upperCase();

  //v-html
  const htmlmessage = '<h2>3. Hello html</h2>';

  //v-bind
  const link = 'https://google.com';
  const message41 = '4.1. v-bind'
  const message42 = '4.2. v-bindの省略形（みんなこう書く）'

  //class
  const isActive5 = true;
  const message5 = "5. v-bindでクラス適用";
  const isBlueActive5 = true;

  //style
  const message6 = "6. styleを指定する";
  const styleObject = {
    color: 'red',
    fontWeight: 900,
  };

  //v-if, v-else-if, v-else
  const error = "エラーが発生しています";
  const stock = 6;

  //v-show
  const error8 = true;

  //v-for
  const languages9 = ['JavaScript', 'TypeScript', 'Vue.js', 'React'];
  const user9 = [
    {id:1, name:'John', email:'jon@test.com', admin: true},
    {id:1, name:'Take', email:'take@test.com', admin: true},
    {id:1, name:'Ika', email:'ika@test.com', admin: false},
    {id:1, name:'Samon', email:'samon@test.com', admin: true},
  ];

  //v-on
  //v-onclick
  let number10 = 0 ;
  const PlussButton = () => {
    number10 = number10 + 1;
    console.log(number10);
  }
  const MinusButton = () => {
    number10 --;
    console.log(number10);
  }

  //event
  const clickButton11 = (event) => {
    console.log(event.target);
  }

  //イベント修飾子
  const send = (event) => {
    event.preventDefault();
    console.log('send');
  }

</script>

<style scoped>
.active{
  color: red;
}
.under_line5{
  text-decoration: underline;
}
.blue5{
  background: blue;
}
</style>

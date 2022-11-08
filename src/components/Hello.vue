<template>
  <h2>Hello Component</h2>
  <button @click="Button"></button>
  <p>text: {{ props.text.num }}</p>
</template>

<script setup>
//defaineProps関数を使ってpropsを受け取る
//型を設定せず、配列で名前を指定することもできる defineProps(['message'])
//const props = defineProps({
  //名前と型（String,Number,Boleanなど）を定義
  //message: String,
//})

//template内でprops.****と書くのが面倒なら、分割代入を使う
const props= defineProps({
  //親からプロパティを渡されない場合のデフォルト設定。typeで型定義、defaultでデフフォルト値を設定
  //name: {type: String, default: 'Default Name'},
  //message: String,
  //age: {
    //type: String,
    //Propsを必ず受け取りたい場合はrequired: tureを使う
    //required: true,
    //required: false,
  //},
  //price: {
    //type: Number,
  //},
  text: {
    type: Object,
  }
});

const Button = () => {
  props.text.num = 200;
}

</script>
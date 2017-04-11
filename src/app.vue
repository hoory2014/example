<template>
  <div>
    <h1 v-html="title"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="{finished:item.isFinished}" @click="toggleFinish(item)">{{item.label}}</li>
    </ul>
    <nv-bottom></nv-bottom>
    <ul class="list-group" v-for="(group,index) in groups">
      <li><span @click="removeTodo(group)">×</span>{{group.text}}{{index}}</li>
    </ul>
    <button @click="addAtLast">在末尾增加一项</button><button @click="deleteAtTop">删除第一项</button><button @click="deleteAtBottom">删除最后一项</button>
  </div>

</template>

<script>
  import Store from './store'
  export default {
    name: 'app',
    data() {
      return {
        title: '<span>1.</span>this is a todolist',
        items: Store.fetch(),
        newItem: '',
        groups:[
          {text: 'item'},
          {text: 'item'},
          {text: 'item'}
        ]
      };
    },
    watch:{
      items:{
        handler(items){
          Store.save(items)
        },
        deep:true
      }
    },
    methods: {
      toggleFinish(item) {
        item.isFinished = !item.isFinished;
      },
      addNew() {
        this.items.push({
          label: this.newItem,
          isFinished: false
        });
        this.newItem = '';
      },
      removeTodo(group) {
          var index=this.groups.indexOf(group);
          this.groups.splice(index,1)
      },
      addAtLast() {
          this.groups.push({text: 'item'})
      },
      deleteAtTop() {
        this.groups.shift()
      },
      deleteAtBottom() {
        this.groups.pop()
      }
    },
    components: {
      'nv-bottom':require('./components/footer.vue')
    }
  };
</script>
<style>
  .finished {
    text-decoration: underline;
  }
  .list-group li{
    height:30px;line-height: 30px;border: 1px solid #ccc;
  }
  .list-group li span{float: right;}
</style>

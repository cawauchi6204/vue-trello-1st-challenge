<template>
  <div>
    <header>
      my Trello
      1周目！！！！
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable :list="lists" class="list-index" @end="movingList">
        <div class="list-index">
          <list v-for="(item,index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
          />
        </div>
        <list-add></list-add>
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from './ListAdd'
import List from './List'
import { mapState } from 'vuex'
  export default {
    components:{
      ListAdd,
      List,
      draggable,
    },
    methods:{
      movingCard() {
        this.$store.dispatch('updateList',{lists:this.lists})
      },
      movingList() {
        this.$store.dispatch('updateList',{lists:this.lists})
      }
    },

    computed: {
      ...mapState([
        'lists'
      ]),
      totalCardCount() {
        return this.$store.getters.totalCardCount
      }
    },
  }
</script>
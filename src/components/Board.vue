<template>
  <!-- ここから追加 -->
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <draggable 
        :list="lists" 
        @end="movingList"
        class="list-index">
        <list v-for="(item, index) in lists" 
          :key="item.id" 
          :title="item.title" 
          :cards="item.cards"
          :listIndex="index" 
          @change="movingCard"
        />
        <list-add/>
        </draggable>
      </div>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import List from './List.vue';
import ListAdd from './ListAdd.vue';
import { mapState } from 'vuex';

export default {
  components: { 
    ListAdd,
    List, 
    draggable
  },
  computed:{
    ...mapState([
      'lists'
    ]),
    totalCardCount(){
      return this.$store.getters.totalCardCount;
    },
  },
  methods:{
    movingCard: function(){
      this.$store.dispatch('updateList', {lists: this.lists})
    },
    movingList: function(){
      this.$store.dispatch('updateList', {lists: this.lists})
    }
  }
}
</script>


<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <draggable :list="lists" @end="movingList" class="list-index">
          <list v-for="(item, index) in lists"
                :key="item.id"
                :title="item.title"
                :cards="item.cards"
                :listIndex="index"
          />
          <list-add/>
        </draggable>
      </div>
    </main>
  </div>
</template>

<script>
import ListAdd from './ListAdd.vue'
import List from './List'
import { mapState } from 'vuex'

export default {
    components: {
        ListAdd,
        List,
    },
    computed: {
      ...mapState([
        'lists'
      ]),
      totalCardCount() {
        return this.$store.getters.totalCardCount
      }
    },
    methods: {
      movingCard: function() {
        this.$store.dispatch('updateList', { lists: this.lists })
      },
      movingList: function() {
        this.$store.dispatch('updateList', { lists: this.lists })
      }
    }
}
</script>
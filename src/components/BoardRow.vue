<template>
    <div class="row"> 
        <template v-for="(casilla, index) in row">
            <BoardSquare 
            :key="index"
            :row="rowNum"
            :col="index"
            :ficha="casilla != null ? fichas.filter(val => val.index == casilla)[0] : null"
            @posibleMove="movimientoDisponible">
            </BoardSquare>

        </template>      
    </div>
</template>

<script>

import BoardSquare from "./BoardSquare.vue";

export default {
  name: 'BoardRow',
  components: { BoardSquare },
  props: ['row', 'rowNum', 'fichas'],
  methods: {
      movimientoDisponible(data){
          this.$emit('posibleMove', data)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row {
    height: 65px;
    display: flex;
    flex-direction: row;
}
</style>
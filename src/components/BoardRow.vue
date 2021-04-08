<template>
    <div class="row"> 
        <template v-for="(casilla, index) in row">
            <BoardSquare 
            :key="index"
            :row="rowNum"
            :col="index"
            :ficha="casilla =! null ? fichas[casilla] : null">
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
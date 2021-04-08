<template>
    <div class="row"> 
        <template v-for="(fila, index) in row">
            <BoardSquare 
            :key="index"
            :row="rowNum"
            :col="index">

            </BoardSquare>

        </template>      
    </div>
</template>

<script>

import BoardSquare from "./BoardSquare.vue";

export default {
  name: 'CheckerBoard',
  components: { BoardSquare },
  props: ['row', 'rowNum'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row {
    height: 65px;
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    flex-direction: row;
}
</style>
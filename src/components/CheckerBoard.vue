<template>
    <div class="board">
      <template v-for="(fila, index) in createBoard">
        <BoardRow :key="index" :row="fila" :rowNum="index">      
        </BoardRow>
      </template>     
    </div>
</template>

<script>

import BoardRow from "./BoardRow.vue";

export default {
  name: 'CheckerBoard',
  components: { BoardRow },
  computed: {
      createBoard() {
        let b = [];

        for (let i = 0; i < 8; i++) {
            b.push(Array(8).fill(null));
        }

        let size = b.length,
        count = 0,
        row = size - 1,
        row2 = 0;

        for (let i = 0; i < 3; i++) {
            for (let col = 0; col < size; col+=2) {
                if (i % 2 === 1) {
                    b[row-i][col+1] = count;
                    b[row2+i][col] = (size/2)*3 + count;
                } else {
                    b[row-i][col] = count;
                    b[row2+i][col+1] = (size/2)*3 + count;
                }
                count++;
            }
        }

        return b;
      }
  },
  methods: {
      llenarBoard(board) {
        let size = board.length,
        count = 0,
        row = size - 1,
        row2 = 0;

        for (let i = 0; i < 3; i++) {
          for (let col = 0; col < size; col+=2) {
              if (i % 2 === 1) {
                  board[row-i][col+1] = count;
                  board[row2+i][col] = (size/2)*3 + count;
              } else {
                  board[row-i][col] = count;
                  board[row2+i][col+1] = (size/2)*3 + count;
              }
              count++;
          }
        }

        return board;
      },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
    width: 550px;
    margin: 0 auto;
    margin-top: 20px;
    margin-bottom: 20px;
    border: 3px solid black;
}
</style>

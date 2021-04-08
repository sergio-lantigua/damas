<template>
    <div class="board">
      <template v-for="(fila, index) in tablero">
        <BoardRow 
        :key="index" 
        :row="fila" 
        :rowNum="index" 
        :fichas="fichas" 
         @posibleMove="movimientoDisponible">      
        </BoardRow>
      </template>     
    </div>
</template>

<script>

import BoardRow from "./BoardRow.vue";

function createBoard() {
        let tablero = [];
        let fichas = [],
        playerOne = 1,
        playerTwo = 2;
        //creando la matriz para el tablero
        for (let i = 0; i < 8; i++) {
            tablero.push(Array(8).fill(null));
        }

        let size = tablero.length,
        count = 0,
        row = size - 1,
        row2 = 0;
        //marcando las posiciones que tendran fichas
        for (let i = 0; i < 3; i++) {
            for (let col = 0; col < size; col+=2) {
                if (i % 2 === 1) {
                    tablero[row-i][col+1] = count;
                    tablero[row2+i][col] = (size/2)*3 + count;
                    //llenado el arreglo de las fichas con la posicion inicial en el tablero
                    fichas.push({index:count , jugador: playerOne, rey: false, row: row-i, col: col+1, eliminado: false});
                    fichas.push({index:(size/2)*3 + count ,jugador: playerTwo, rey: false, row: row2+i, col: col, eliminado: false});
                } else {
                    tablero[row-i][col] = count;
                    tablero[row2+i][col+1] = (size/2)*3 + count;
                    fichas.push({index:count , jugador: playerOne, rey: false, row: row-i, col: col, eliminado: false});
                    fichas.push({index:(size/2)*3 + count ,jugador: playerTwo, rey: false, row: row2+i, col: col+1, eliminado: false});
                }
                count++;
            }
        }

        return {tablero, fichas};
}

export default {
  name: 'CheckerBoard',
  components: { BoardRow },
  data() {
      let completeBoard = createBoard();
      return {
        tablero: completeBoard.tablero,
        fichas: completeBoard.fichas,
        fichaSeleccionada: null
      }
  },
  updated(){
      console.log("se actualizao el componentew")
  },
  methods: {
    movimientoDisponible(fichaIndex){
        let simpleMoves = [],
        ficha = this.fichas.filter(val => val.index == fichaIndex)[0];

        let fila =  ficha.jugador == 1 ? ficha.row - 1 : ficha.row + 1,
            casillaIzquierda = ficha.col -1,
            casillaDerecha = ficha.col + 1;

        simpleMoves = this.casillasDisponibles(fila, casillaIzquierda, casillaDerecha);
        console.log(simpleMoves);
        return simpleMoves;
    },
    casillasDisponibles(fila, casillaIzquierda, casillaDerecha){
        let movimientos = [];

        if (fila >= this.tablero.length || fila < 0) {
            return movimientos;
        }

        if (this.tablero[fila][casillaIzquierda] === null) {
            movimientos.push({fila: fila, col: casillaIzquierda});
        }

        if (this.tablero[fila][casillaDerecha] === null) {
            movimientos.push({fila: fila, col: casillaDerecha});
        }

        return movimientos;
    },
    posiblesSaltos(fichaIndex, jugador){
      let saltosDisponibles = [],
      ficha = fichas.filter(val => val.index == fichaIndex)[0];

      let fila = ficha.jugador == 1 ? ficha.row - 1 : ficha.row + 1,
          casillaIzquierda = ficha.col -1,
          casillaDerecha = ficha.col + 1,
          proximaFila = ficha.jugador == 1 ? fila - 1 : fila + 1,
          proximaCasillaIzquierda = casillaIzquierda - 1 ,
          proximaCasillaDerecha = casillaDerecha + 1;
          
      let casillaIzquierdaAdjacente = board[fila][casillaIzquierda];

      if (casillaIzquierdaAdjacente != null && board[casillaIzquierdaAdjacente].jugador !== jugador) {
            if (this.board[proximaFila][proximaCasillaIzquierda] === null) {
                saltosDisponibles.push({row: proximaFila, col: proximaCasillaIzquierda});
            }
        }

      let casillaDerechaAdjacente = board[fila][casillaDerecha];
      
      if (casillaDerechaAdjacente != null && board[casillaDerechaAdjacente].jugador !== jugador) {
            if (this.board[proximaFila][proximaCasillaDerecha] === null) {
                saltosDisponibles.push({row: proximaFila, col: proximaCasillaDerecha});
            }
        }

      return saltosDisponibles
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
    width: 600px;
    margin: 0 auto;
    margin-top: 20px;
    margin-bottom: 20px;
}
</style>

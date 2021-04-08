<template>
    <div  :class="colorCuadro">
        <BoardChips @posibleMove="movimientoDisponible" :value="ficha"></BoardChips>
    </div>
</template>

<script>
import BoardChips from "./BoardChips.vue";

export default {
  name: 'BoardSquare',
  components: { BoardChips },
  props: ['row', 'col', 'ficha'],
  computed: {
    colorCuadro() {
        let color = (this.row + this.col) % 2 === 0 ? "light-brown" : "dark-brown",
        classes = "cuadro " + color;
        return classes;
    }
},
methods: {
    clickSquare() {
        console.log(this.row)
    },
    movimientoDisponible(data){
        this.$emit('posibleMove', data)
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .cuadro {
        cursor: pointer;
        flex-grow: 1;
        flex-basis: 0;
        display: flex;
        justify-content: center;
        -ms-flex-align: center;
        align-items: center;
    }

    .dark-brown {
    background-color: rgb(179 124 62 / 96%);;
    }

    .light-brown {
        background-color: rgb(255 222 176);
    }
</style>
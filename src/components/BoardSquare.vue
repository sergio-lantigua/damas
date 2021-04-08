<template>
    <div :class="colorCuadro"></div>
</template>

<script>
export default {
  name: 'BoardSquare',
  props: ['row', 'col'],
  methods: {
        getColor() {
        if ((Number(this.row) + Number(this.col)) % 2 == 0) {
            return 'white';
        } else {
            return 'black';
        }
        }
    },
   computed: {
        colorCuadro() {
            let color = (this.row + this.col) % 2 === 0 ? "red" : "white",
            classes = "square " + color;
            return classes;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .square {
        cursor: pointer;
        flex-grow: 1;
        flex-basis: 0;
        display: flex;
        justify-content: center;
        -ms-flex-align: center;
        align-items: center;
        border: 2px solid gray;
    }

    .red {
    background-color: black;
    }

    .black {
        background-color: white;
    }
</style>
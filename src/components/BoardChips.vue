<template>
    <div @click="clickFicha" :class="colorCuadro"></div>
</template>

<script>
export default {
  name: 'BoardSquare',
  props: ['value'],
  computed: {
    colorCuadro() {
        let estilos = "";
        
        if (this.value) {
            if (this.value.jugador === 1){
                estilos += "player-red";
            }else if (this.value.isKing) {
                estilos += " is a king";
            }else{
                estilos += "player-white";
            }
        } 

        return estilos;
    }
},
methods: {
    clickFicha() {
        this.$emit("posibleMove", this.value.index)
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.player-red, .player-white {
    border-radius: 50%;
    width: 70%;
    height: 70%;
    border: 2px solid black;
}

.player-red {
    background-color: red;
}

.player-white {
    background-color: white;
}
</style>
<template>
    <img :src="queen" @click="pieceClick">
</template>

<script>

export default {
    name : "queen",
    data () {
        return {
            queen : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.queen = require("../assets/chess-queen-" + this.color + ".png")
    },
    methods : {
        pieceClick : function() {
            this.$emit('clickPiece','queen', this['data-x'], this['data-y'])
        }
    }
}   
</script>

<style scoped>
img {
    width: 50px;
    height: 50px;
    display: flex;  
}
* {
    padding: 0;
    margin: 0;
}
</style>
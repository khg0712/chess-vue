<template>
    <img :src="king" @click="pieceClick">
</template>

<script>

export default {
    name : "king",
    data () {
        return {
            king : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.king = require("../assets/chess-king-" + this.color + ".png")
    },
    methods: {
        pieceClick : function() {
            this.$emit('clickPiece','king', this['data-x'], this['data-y'])
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
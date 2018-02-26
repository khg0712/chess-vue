<template>
    <img :src="pawn" @click="pieceClick">
</template>

<script>

export default {
    name : "pawn",
    data () {
        return {
            pawn : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.pawn = require("../assets/chess-pawn-" + this.color + ".png")
    },
    methods : {
        pieceClick : function(){
            this.$emit('clickPiece','pawn', this['data-x'], this['data-y'])
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
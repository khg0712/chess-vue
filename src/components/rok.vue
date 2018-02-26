<template>
    <img :src="rok" @click="pieceClick">
</template>

<script>

export default {
    name : "rok",
    data () {
        return {
            rok : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.rok = require("../assets/chess-rok-" + this.color + ".png")
    },
    methods : {
        pieceClick : function() {
            this.$emit('clickPiece','rok', this['data-x'], this['data-y'])
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
</style>
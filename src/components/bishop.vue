<template>
    <img :src="bishop" @click="pieceClick">
</template>

<script>
export default {
    name : "bishop",
    data () {
        return {
            bishop : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.bishop =  require("../assets/chess-bishop-" + this.color + ".png")
    },
    methods : {
        pieceClick : function() {
            this.$emit('clickPiece','bishop', this['data-x'], this['data-y'])
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
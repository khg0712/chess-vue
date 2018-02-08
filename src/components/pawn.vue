<template>
    <img :src="pawn">
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
<template>
    <img :src="knight">
</template>

<script>

export default {
    name : "knight",
    data () {
        return {
            knight : ""
        }
    },
    props : ['color','data-x','data-y'],
    created : function() {
        this.knight = require("../assets/chess-knight-" + this.color + ".png")
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
<template>
    <img :src="bishop">
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
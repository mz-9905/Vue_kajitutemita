<template>
    <div id="app" class=".container">
        <div class="example">
            <h1>test</h1>
        </div>
        <HelloWorld/>
    </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default{
    name:"App",
    components:{ HelloWorld }
}
</script>

<style scoped>
.example {
    color: red;
    text-align: center;
}
</style>
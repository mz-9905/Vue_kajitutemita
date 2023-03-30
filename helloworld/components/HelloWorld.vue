<template>
    <div class="m-3 p-3">
        <h1>{{appName}}</h1>
    </div>
</template>

<script>
export default {
    name: "HelloWorld",
    data(){
        return {
            appName:"Hello Vue.js!"
        }
    }
}
</script>
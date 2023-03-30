<template>
    <div class="p-3">
        <h1>{{appName}}</h1>
        <div class="mb-3">{{message}}</div>
        <div class="mb-3">
            計算式: {{kg}} / ({{cm}} * 0.01)^2<br/>
            BMI値: {{bmi}}
        </div>
    </div>
</template>

<script>
export default {
    props:['appName','message','kg','cm','bmi'],
}
</script>
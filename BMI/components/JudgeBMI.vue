<template>
    <div class="p-3">
        <div v-if="bmi<=0.0" class="p-3 mb-2 bg-light bg-gradient text-dark">-</div>
        <div v-else-if="bmi<18.5" class="p-3 mb-2 bg-success bg-gradient text-white">やせ</div>
        <div v-else-if="bmi<25.0" class="p-3 mb-2 bg-primary bg-gradient text-white">標準</div>
        <div v-else-if="bmi<30.0" class="p-3 mb-2 bg-warning bg-gradient text-white">軽度肥満</div>
        <div v-else class="p-3 mb-2 bg-danger bg-gradient text-white">重度肥満</div>
    </div>
</template>

<script>
export default {
    props:['bmi'],
}
</script>
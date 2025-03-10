<script setup>
</script>

<template>
    <div class="loading">Загружаем данные..</div>
</template>

<style>
.loading {
    width: 210px;
    height: 40px;
    line-height: 37px;
    text-align: center;
    border-radius: 35px 15px;
    margin: 20px auto;
    opacity: 0;
    color: #fff;
    animation: loading;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    background: rgba(14, 14, 15, 0.9) !important;
}

@keyframes loading {
    0% {
        opacity: 0;
    } 100% {
        opacity: 1;
    }
}
</style>
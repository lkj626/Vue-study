<template>
  <div class="progress"></div>
</template>

<script>
export default {

}
</script>

<style scoped>
.progress {
    height: 5px;
    background-color: lime;
    width: 0%;
    animation: loading 1s linear;
}

@keyframes loading {
    0% {
        width: 0%;
    }
    50% {
        width: 50%;
    }
    100% {
        width: 100%;
    }
}

</style>
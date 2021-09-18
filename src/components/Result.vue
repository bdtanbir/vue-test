<template>
    <div class="reaction-timer-result">
        <h1>
            Reaction Time: <strong>{{score}}ms</strong>
        </h1>
    </div>
</template>

<script>
export default {
    props: ['score']
}
</script>

<style>
    .reaction-timer-result h1 strong {
        color: #42b983;
    }
</style>

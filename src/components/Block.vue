<template>
    <div v-if="showBlock" @click="stopPlaying" class="reaction-timer-box">
        <h1>Click Me</h1>
    </div>
</template>

<script>
export default {
    props: ['delay'],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true;
            this.startTimer();
        }, this.delay);
    },
    methods: {
        startTimer: function() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            }, 10)
        },
        stopPlaying: function() {
            clearInterval(this.timer);
            this.$emit('end', this.reactionTime);
        }
    }
}
</script>

<style scoped>
    .reaction-timer-box {
        width: 200px;
        height: 200px;
        margin: 20px auto auto auto;
        background: #42b983;
        color: #fff;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border-radius: 4px;
    }
    .reaction-timer-box:active {
        transform: scale(0.98);
    }
</style>
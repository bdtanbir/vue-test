<template>
    <div class="simple-reaction">
        <h1>Simple Reaction Timer</h1>
        <button class="play-reactiontimer" @click="playGame" :disabled="isPlaing">
            Play
        </button>
        
        <Block v-if="isPlaing" @end="endGame" :delay="delay" />

        <Result v-if="isResult" :score="score" />
    </div>
</template>

<script>
import Block from '@/components/Block.vue';
import Result from '@/components/Result.vue';

export default {
    components: {
        Block,
        Result
    },
    data() {
        return {
            isResult: false,
            isPlaing: false,
            delay: '',
            score: ''
        }
    },
    methods: {
        playGame: function() {
            this.isPlaing = true;
            this.isResult = false;
            this.delay = 2000 + Math.random() * 5000;
        },
        endGame: function(reactionTime) {
            this.isResult = true;
            this.isPlaing = false;
            this.score = reactionTime;
        }
    }
}
</script>

<style>
.simple-reaction {
    width: 100%;
    margin: 20px 0 20px 0;
    border: 1px solid #eee;
    text-align: center;
    padding: 30px 0;
    border-radius: 8px;
}
    
</style>
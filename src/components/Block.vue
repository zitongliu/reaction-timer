<template>
    <div v-if="showBlock" class="block" @click="stopTimer">Click me</div>
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
            console.log('mounted')
            setTimeout(() => {
                this.showBlock = true;
                this.startTimer();
            }, this.delay)
        },
        updated() {
            console.log('updated')
        },
        unmounted() {
            console.log('unmounted')
        },
        methods: {
            startTimer() {
                this.timer = setInterval(() => {
                    this.reactionTime += 10;
                }, 10);
            },
            stopTimer() {
                clearInterval(this.timer);
                console.log('reaction time', this.reactionTime);
                this.$emit('end', this.reactionTime);
            }
        }
    }
</script>


<style>
    .block {
        width: 400px;
        background: dodgerblue;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>
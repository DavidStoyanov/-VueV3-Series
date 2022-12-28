<template>
    <div class="block" v-bind:class="stateClasses" @click="whenClick">
        <p v-if="(state == this.flags.WAIT)">Wait...</p>
        <p v-else-if="(state == this.flags.ACT)">*Click me*</p>
    </div>
</template>
  
<script>
export default {
    props: [
        'delay'
    ],
    data() {
        return {
            flags: { WAIT: 'wait', ACT: 'act' },
            state: null,
            timeout: null,
            reactionTime: null,
            startTime: null 
        }
    },
    methods: {
        startTimer() {
            this.startTime = Date.now()
        },
        stopTimer() {
            const dateNow = Date.now()
            this.reactionTime = dateNow - this.startTime
        },
        whenClick() {
            this.stopTimer()

            if (this.state == this.flags.WAIT) {
                this.$emit('gameover')
            } else if (this.state == this.flags.ACT) {
                this.$emit('gameover', this.reactionTime)
            }
        }
    },
    computed: {
        stateClasses() {
            switch (this.state) {
                case this.flags.WAIT: 
                    return { 'click-wait': true }
                case this.flags.ACT:
                    return { 'click-act': true }
                default:
                    return {}
            }
        }
    },
    mounted() {
        this.state = this.flags.WAIT
        this.timeout = setTimeout(() => {
            this.startTimer()
            this.state = this.flags.ACT
        }, this.delay);
    },
    unmounted() {
        this.state = null
    }
}
</script>
  
<style>
    .block {
        width: 400px;
        border-radius: 20px;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
    .click-act {
        background:  #0faf87;
    }
    .click-wait {
        background:  #778884;
    }
	.blink-bg{
		color: #fff;
		padding: 10px;
		display: inline-block;
		border-radius: 5px;
		
	}
</style>
  
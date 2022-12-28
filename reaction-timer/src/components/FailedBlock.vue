<template>
    <div class="block" v-bind:class="stateClasses">
        <p>Failed!</p>
    </div>
</template>
  
<script>
export default {
    props: [
        'delay'
    ],
    data() {
        return {
            
        }
    },
    methods: {
        
    },
    computed: {
        stateClasses() {
            return {
                'click-fail': true
            }
        }
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

	.blink-bg{
		color: #fff;
		padding: 10px;
		display: inline-block;
		border-radius: 5px;
		
	}
    
    .click-fail {
        background:  #af0f2f;
        animation: blinkingBackground 2s infinite;
    }

	@keyframes blinkingBackground{
		0%		{ background-color: #af0f2f;}
		10%		{ background-color: #778884;}
		20%		{ background-color: #af0f2f;}
		40%		{ background-color: #778884;}
        60%	    { background-color: #af0f2f;}
        80%	    { background-color: #778884;}
	}
</style>
  
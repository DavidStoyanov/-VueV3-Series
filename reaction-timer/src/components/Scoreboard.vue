<template>
    <h2>Leader score board</h2>
    <div class="best-worst-box">
        <div>
            <h3>Best Score</h3>
            <p>Score: {{ bestScore.score }}</p>
            <p>Date: {{ dateFormat(bestScore.datetime) }}</p>
        </div>
        <div>
            <h3>Worst Score</h3>
            <p>Score: {{ worstScore.score }}</p>
            <p>Date: {{ dateFormat(worstScore.datetime) }}</p>
        </div>
    </div>
    <div class="score-box">
        <div class="score-item" v-for="item in scoreList" :key="item" >
            <p>Score: {{ item.score }}</p>
            <p>Date: {{ dateFormat(item.datetime) }}</p>
        </div>
    </div>
</template>

<script>
import moment from 'moment'

export default {
    data() {
        return {
            bestScore: {
                score: Number.MAX_SAFE_INTEGER,
                datetime: null
            },
            worstScore: {
                score: Number.MIN_SAFE_INTEGER,
                datetime: null
            }
        }
    },
    props: {
        scoreList: Object
    },
    mounted() {
        this.scoreList.forEach(x => {
            if (x.score < this.bestScore.score) {
                this.bestScore = x
            }
            if (x.score > this.worstScore.score) {
                this.worstScore = x
            }
        });
    },
    methods: {
        dateFormat: function (datetime) {
            return moment(datetime).format('LTS');
        }
    }
}
</script>

<style>
.score-box {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    justify-items: flex-start
}

.score-item {
    border: 3px solid #000;
    border-radius: 10%;
    width: 200px;
    height: 100px;
    margin: 10px;
}

.best-worst-box {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-around;
    margin: 3rem;
}

@media only screen and (max-width: 400px) {
    .best-worst-box > * {
        padding: 0.2rem 0.6rem;
        border-radius: 0.5rem;
    }
}

.best-worst-box > * {
    background: #0faf87;
    opacity: 0.9;
    padding: 0.75rem 5rem;
    border-radius: 3rem;
}

.best-worst-box > * {
    background: #0faf87;
    opacity: 0.9;
    padding: clamp(0.2rem 0.6rem, 0.75rem 5rem);
    border-radius: 3rem;
} 

.best-box {

}

.worst-box {

}


</style>
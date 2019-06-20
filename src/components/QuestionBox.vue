<template>
    <div>
        <b-jumbotron>
            <template>
                {{currentquestion.question}}
            </template>

            <hr class="my-4">

            <b-list-group class="list-group">
                <b-list-group-item
                v-for="(answer, index) in answers" :key="index"
                @click.prevent="selectAnswer(index)"
                :class="[selectedIndex === index ? 'selected' : '']"
                >
                 {{ answer }}
                </b-list-group-item>
            </b-list-group>


            <b-button variant="primary" href="#" class="btn">Submit</b-button>
            <b-button @click="next" variant="primary" href="#" class="btn">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash'

export default {
    props: {
        currentquestion: Object,
        next: Function
    },
    data(){
        return{
            selectedIndex: null,
            shuffledAnswers: []
        }
    },
    computed: {
        answers() {
            let answers = [...this.currentquestion.incorrect_answers]
            answers.push(this.currentquestion.correct_answers)
            return answers
        }
    },
    watch: {
      currentquestion(){
          this.selectedIndex = null
          this.shuffleAnswers()
      }
    },
    methods:{
        selectAnswer(index){
            this.selectedIndex = index
        },
        shuffleAnswers() {
            let answers = [...this.currentquestion.incorrect_answers, this.currentquestion.correct_answers]
            this.shuffledAnswers = _.shuffle(answers)
        }
    }
}
</script>

<style scoped>
.list-group{
    margin-bottom: 15px;
}

.list-group :hover{
    background-color: #ddd;
    cursor: pointer;
}

.btn{
    margin: 5px
}

.selected {
    background-color: aquamarine;
}

.correct{
    background-color: lightgreen;
}

.wrong{
    background-color: lightsalmon;
}

</style>

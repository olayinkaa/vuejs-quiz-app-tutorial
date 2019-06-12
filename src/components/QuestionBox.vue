<template>
        <b-jumbotron>
                <template slot="lead">
                   {{currentQuestion.question}}
                </template>

                <hr class="my-4">

                <!-- <p v-for="answer in answers" :key="answer.id">
                    {{ answer }}
                </p> -->
                <b-list-group  >           
                    <b-list-group-item class="list-group-item"
                        v-for="(answer,index) in answers" 
                        :key="index"
                        @click.prevent="selectAnswer(index)" 
                        :class="[
                        !answered && selectedIndex===index ? 'selected':
                        answered && correctIndex ===index ? 'correct':
                        answered && selectedIndex===index && correctIndex!==index ? 'incorrect':''
                        ]"
                    >
                    {{ answer }}
                    </b-list-group-item>
                </b-list-group>
               
                <b-button variant="primary" 
                @click="submitAnswer" 
                :disabled="selectedIndex===null || answered"
                class="mr-3 mt-3">Submit</b-button>
                <b-button variant="success" class="mt-3" href="#" @click="next">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
    import _ from 'lodash'

    export default {
        name:"QuestionBox",
        props:{
            currentQuestion: Object,
            next: Function,
            increment: Function
        },
        data(){

                return {

                    selectedIndex: null,
                    correctIndex : null,
                    shuffleAnswers: [],
                    answered: false

                }
        },
        watch: {

                    currentQuestion : {

                        immediate: true,
                        handler(){

                                this.selectedIndex = null
                                this.answered = false
                                this.shuffleAnswers()
                        }
                    }

            /*
                currentQuestion: function(){
                    this.selectedIndex = null
                    this.shuffleAnswers()
                },
              
            */
        },
        computed : {

            answers: function(){

                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
            }
        },
        methods : {

            selectAnswer(index){

                    this.selectedIndex = index
            },

            submitAnswer: function(){

                    let isCorrect = false
                    if(this.selectedIndex===this.correctIndex)
                    {
                        isCorrect = true
                    }

                    this.increment(isCorrect)
            },
            shuffleAnswers() {

                        let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
                        this.shuffleAnswers = _shuffle(answers)
                        this.correctIndex = this.shuffleAnswers.indexOf(this.currentQuestion.correct_answer)
            }
        }
    }
</script>

<style  scoped>

.list-group-item:hover{
        background: rgb(245, 245, 245);
        /* color:white; */
        cursor: pointer;
}

.selected {
        background: black;
        color: white;
}
.correct{
    background: green;
}

.incorrect{
    background: red;
}


</style>
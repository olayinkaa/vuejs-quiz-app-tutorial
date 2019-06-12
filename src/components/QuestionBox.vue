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
                    <b-list-group-item 
                        v-for="(answer,index) in answers" 
                        :key="index">
                        
                    {{ answer }}
                    </b-list-group-item>
                </b-list-group>
               
                <b-button variant="primary" class="mr-3 mt-3" href="#">Submit</b-button>
                <b-button variant="success" class="mt-3" href="#" @click="next">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
    export default {
        name:"QuestionBox",
        props:{
            currentQuestion: Object,
            next: Function
        },
        computed : {

            answers: function(){

                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
<template>
    <div>
        <b-nav>
            <b-nav-item disabled>fancy Quiz APP</b-nav-item>
            <b-nav-item disabled>Counter {{numCorrect}}/{{numTotal}}</b-nav-item>
        </b-nav>
    </div>
</template>

<script>
    export default {
        name: "Header",
        props: {

                numCorrect:Number,
                numTotal:Number
        }
        
    }
</script>

<style lang="scss" scoped>

</style>
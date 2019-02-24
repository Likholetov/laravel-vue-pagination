<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">Topics</div>

                    <div class="card-body">
                        <pagination v-if="meta && topics.length" for="topics" :pagination="meta.pagination"></pagination>
                        <topic v-for="topic in topics" :topic="topic" :key="topic.id"></topic>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import eventHub from "../events.js"

    export default {
        data() {
            return {
                topics: [],
                meta: null
            }
        },
        methods:{
            getTopics(page){
                axios.get(`/topics?page=${page}`)
                .then(responce => {
                    this.topics = responce.data.data
                    this.meta = responce.data.meta
                })
                .catch(e => {
                    console.log(e)
                })
            }
        },
        mounted() {
            this.getTopics(1)

            eventHub.$on('topics.switched-page', this.getTopics)
        }
    }
</script>

<template>
    <div class="media">
        <img class="align-self-start mr-3" :src="topic.user.data.avatar">
        <div class="media-body">
            <h5 class="mt-0">{{ topic.title }}</h5>
            <p>by {{ topic.user.data.name }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        props: [
            'topic'
        ]
    }
</script>


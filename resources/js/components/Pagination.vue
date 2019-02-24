<template>
    <nav aria-label="Page navigation example">
    <ul class="pagination">
        <li class="page-item" :class="{ 'disabled' : !pagination.links.previous}">
        <a class="page-link" href="#" aria-label="Previous" @click.prevent="switchPage(pagination.current_page - 1)">
            <span aria-hidden="true">&laquo;</span>
            <span class="sr-only">Previous</span>
        </a>
        </li>
        <li class="page-item" :class="{'active': pagination.current_page === page}" v-for="page in parseInt(pagination.total_pages)" :key="page">
            <a class="page-link" href="#" @click.prevent="switchPage(page)">{{ page }}</a>
        </li>
        <li class="page-item" :class="{ 'disabled' : !pagination.links.next}">
        <a class="page-link" href="#" aria-label="Next" @click.prevent="switchPage(pagination.current_page + 1)">
            <span aria-hidden="true">&raquo;</span>
            <span class="sr-only">Next</span>
        </a>
        </li>
    </ul>
    </nav>
</template>

<script>
    import eventHub from "../events.js"

    export default {
        props: {
            pagination: Object,
            for: {
                type: String,
                default: 'default'
            }
        },
        methods: {
            switchPage(page){
                if (page < 1 || page > this.pagination.total_pages) {
                    return
                }

                eventHub.$emit(this.for + '.switched-page', page)
            }
        }
    }
</script>


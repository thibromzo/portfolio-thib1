<script setup>
    defineProps ({
        articleContent: Object
    });

    const emit = defineEmits(["creationClicked"]);

    function onCreationClick(creationName) {
        emit("creationClicked", creationName);
    };
</script>

<template>
    <article @click="onCreationClick(articleContent.name)" class="col-flex-wrap-center">
        <figure>
            <img :src="'/pictures/' + articleContent.imgSrc"
                 :title="articleContent.imgTitle"
                 :alt="articleContent.imgAlt">
        </figure>
        <h2>{{ articleContent.title }}</h2>
    </article>
</template>

<style scoped>
    article {
        padding-left: 1.1rem;
        padding-right: 1.1rem;
        margin-bottom: 1rem;
        border-radius: 5% 15%;
    }

    article:hover {
        box-shadow: 5px 5px 10px black;
    }
    
    figure {
        width: 150px;
        height: 150px;
        margin-top: 30px;
    }

    img {
        box-shadow: 0 0 15px black;
    }
</style>
<template>
    <div class="post">

       <div>
            <div class="post__title"><strong>Title:</strong> {{ post.title }}</div>
            <div class="post__description"><strong>Description:</strong> {{ post.body }}</div>
       </div>

       <div class="post__btns">
           <my-button
            @click="$emit('remove', post)"
           >
               Delete
            </my-button>
       </div>
    </div>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true,
        }
    }
}
</script>

<style lang="sass" scoped>
.post
    display: flex
    align-items: center
    justify-content: space-between
    padding: 15px
    margin-top: 15px
    border: 2px solid teal
</style>
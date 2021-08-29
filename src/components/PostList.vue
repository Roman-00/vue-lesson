<template>
    <div v-if="posts.length > 0">
        <h3>Post List</h3>
        <transition-group name="post-list">
            <post-item 
                v-for="post in posts"
                :post="post"
                :key="post.id"
                @remove="$emit('remove', post)"
            />
        </transition-group>
    </div>
    <h2 v-else style="color: red">
        List Post Not Found
    </h2>
</template>

<script>
import PostItem from './PostItem.vue'
export default {
  components: { PostItem },
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style lang="sass" scoped>
.post-list-item
    display: inline-block
    margin-right: 10px
.post-list-enter-active,
.post-list-leave-active
    transition: all .5s ease
.post-list-enter-from,
.post-list-leave-to
    opacity: 0
    transform: translateY(30px)
.post-list-move
    transition: transform .4s ease
</style>
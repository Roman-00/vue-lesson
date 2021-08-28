<template>
    <form @submit.prevent>
        <h4>Add a new Post</h4>
        
        <my-input 
            v-model="post.title"
            type="text" 
            placeholder="Title"
        />

        <my-input
            v-model="post.body" 
            type="text" 
            placeholder="Description"
        />

        <my-button 
            style="align-self: flex-end"
            @click="createPost" 
        >
            Add Post
        </my-button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
                title: '',
                body: ''
            }
        }   
    }
}
</script>

<style lang="sass" scoped>
form
    display: flex
    flex-direction: column
</style>
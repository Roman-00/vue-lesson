<template>

    <div class="app" id="app">

        <div class="container">

            <form>
                <h4>Add a new Post</h4>
                
                <input 
                    v-bind:value="title"
                    @input="title = $event.target.value"
                    class="input" 
                    type="text" 
                    placeholder="Title"
                >

                <input 
                    v-bind:value="body"
                    @input="body = $event.target.value"
                    class="input" 
                    type="text" 
                    placeholder="Description"
                >

                <button class="btn" @click="createPost">Add Post</button>
            </form>

            <div class="post" v-for="post in posts">
                <div class="post__title"><strong>Title:</strong> {{ post.title }}</div>
                <div class="post__description"><strong>Description:</strong> {{ post.body }}</div>
            </div>

        </div>

    </div>

</template>

<script>
export default {
    data() {
        return {
            posts: [
                {id: 1, title: 'Post as JavaScript', body: 'JavaScript a programming language'},
                {id: 2, title: 'Post as JavaScript 2', body: 'JavaScript a programming language 2'},
                {id: 3, title: 'Post as JavaScript 3', body: 'JavaScript a programming language 3'}
            ],
            title: '',
            body: ''
        }
    },
    methods: {
        createPost() {

        }
    }
}
</script>

<style lang="sass">
*
    margin: 0
    padding: 0
    box-sizing: border-box
.app
    padding-top: 20px
.container
    max-width: 1100px
    margin: 0 auto;

.post
    padding: 15px
    margin-top: 15px
    border: 2px solid teal
.input
    width: 100%
    margin-top: 15px
    padding: 10px 15px
    border:  1px solid teal
form
    display: flex
    flex-direction: column
.btn
    align-self: flex-end
    margin-top: 15px
    padding: 10px 15px
    background: none
    color: teal
    border: 1px solid teal
    cursor: pointer
</style>
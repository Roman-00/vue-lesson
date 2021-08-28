<template>

    <div class="app" id="app">

        <div class="container">

            <post-form
                @create="createPost"
            />

            <post-list 
                :posts="posts"
                @remove="removePost"
            />

        </div>

    </div>

</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'

export default {
    components: {
        PostForm,
        PostList
    },
    data() {
        return {
            posts: [
                {id: 1, title: 'Post as JavaScript', body: 'JavaScript a programming language'},
                {id: 2, title: 'Post as JavaScript 2', body: 'JavaScript a programming language 2'},
                {id: 3, title: 'Post as JavaScript 3', body: 'JavaScript a programming language 3'}
            ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
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
</style>
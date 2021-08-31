<template>

    <div>

        <my-input
            v-model="searchQuery"
            placeholder="Search..."
        />

        <div class="app__btns">

            <my-button
                @click="showDialog"
            >
                App Post
            </my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
            />

        </div>

        <my-dialog v-model:show="dialogVisible">
            <post-form
                @create="createPost"
            />
        </my-dialog>

        <post-list 
            :posts="sortedAndSearchedPosts"
            @remove="removePost"
            v-if="!isPostLoading"
        />
        <div v-else>Loading ...</div>

        <div 
            ref="observer"
            class="observer"
        >

        </div>

        <!-- div class="page__wrapper">
            <div 
                v-for="pageNumber in totalPages" 
                :key="pageNumber" 
                class="page"
                :class="{
                    'page__current': page === pageNumber
                }"
                @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div -->

    </div>

</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import axios from 'axios'

export default {
    components: {
        PostForm,
        PostList
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'Sort by Title'},
                {value: 'body', name: 'Sort by Description'}
            ],
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        /*changePage(pageNumber) {
            this.page = pageNumber
        },*/
        async fetchPosts() {
            try {
                this.isPostLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10', {
                    _page: this.page,
                    _limit: this.limit
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = response.data;
            }
            catch (e) {
                console.log('Erorr');
            }
            finally {
                this.isPostLoading = false;
            }
        },

        async loadMorePosts() {
            try {
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10', {
                    _page: this.page,
                    _limit: this.limit
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = [...this.posts, ...response.data];
            }
            catch (e) {
                console.log('Erorr');
            }
        }
    },
    mounted() {
        this.fetchPosts();
        console.log(this.$refs.observer);

        const options = {
            rootMargin: '0px',
            threshold: 1.0
        }

        const callback = (entries, observer) => {
            if (entries[0].isIntersecting && this.page < this.totalPages) {
                this.loadMorePosts()
            }
        };

        const observer = new IntersectionObserver(callback, options);
        observer.observe(this.$refs.observer);

    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((a, b) => {
                return a[this.selectedSort]?.localeCompare(b[this.selectedSort])
            })
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    watch: {
        /*selectedSort(newValue) {
            this.posts.sort((a, b) => {
                return a[this.selectedSort]?.localeCompare(b[this.selectedSort])
            })
        }
        page() {
            this.fetchPosts()
        }*/
    }
}
</script>

<style lang="sass">
.page
    padding: 10px
    border: 1px solid teal
    &__wrapper
        display: flex
        margin-top: 15px
    &__current
        border: 2px solid orange
.observer
    height: 30px
    background-color: red
</style>
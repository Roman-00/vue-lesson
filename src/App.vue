<template>

    <div class="app">
        <NavBar>

        </NavBar>
        <div class="container">
            <router-view />
        </div>
    </div>

</template>
<script>
import NavBar from '@/components/NavBar';
export default {
    components: {
        NavBar
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
    &__btns
        display: flex
        justify-content: space-between
        align-items: center
        margin:  20px 0
.container
    max-width: 1100px
    margin: 0 auto;
</style>
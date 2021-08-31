<template>

    <header id="header" class="header">

        <div class="navbar">

            <div>Vue 3</div>

            <div class="navbar__btns">

                <my-button @click="$router.push('/posts')" class="navbar__btns--item">
                    Посты
                </my-button>
                <my-button @click="$router.push('/about')" class="navbar__btns--item">
                    О нас
                </my-button>

            </div>

        </div>

    </header>

</template>
<script>
export default {


}
</script>
<style lang="sass" scoped>
.navbar
    display: flex
    align-items: center
    height: 50px
    padding: 0 15px
    background-color: lightgrey
    box-shadow: 2px 2px 4px gray
    &__btns
        margin-left: auto
</style>
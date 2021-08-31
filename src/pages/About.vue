<template>

    <section class="about">

        <h2 class="about__title">
            Страница о нас
        </h2>

         <router-link to="/">
            Главная
        </router-link>

        <router-link to="/posts">
            Посты
        </router-link>

    </section>

</template>
<script>
export default {
    
}
</script>
<style lang="sass" scoped>
.about
    position: relative
    &__title
        color: red
        font-size: 20px
</style>
<template>
    <div class="dialog" v-if="show" @click="hideDialog">

        <div class="dialog__content" @click.stop>
            <slot></slot>
        </div>

    </div>
</template>

<script>
export default {
    name: 'my-dialog',
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog(e) {
            this.$emit('update:show', false);
        }
    }
}
</script>

<style lang="sass">
.dialog
    position: fixed
    top: 0
    bottom: 0
    right: 0
    left: 0
    display: flex
    background: rgba(0, 0, 0, 0.5) 
    &__content
        min-width: 300px
        min-height: 50px
        margin: auto
        padding: 20px
        background-color: white
        border-radius: 12px
</style>
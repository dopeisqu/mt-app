<template>
    <div class="m-user">
        <template v-if="user">
            欢迎您，<span class="username">{{ user }}</span>
            [<nuxt-link to="/exit">退出</nuxt-link>]
        </template>
        <template v-else>
            <nuxt-link class="register" to="/register">立即登录</nuxt-link>
        </template>
    </div>
</template>

<script>
export default {
    data() {
        return {
            user:'tyqu'
        }
    }
}
</script>

<style lang='scss'>

</style>
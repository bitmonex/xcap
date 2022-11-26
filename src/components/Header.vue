<template>
    <div class="head">
        <span><a v-for="menu in menus" :key="menu.title" :href="menu.url" :class="{logo: menu.logo}">{{menu.title}}</a></span>
    </div>

</template>

<script>
export default{
    data(){
        return{
            menus:[
                {title: 'xcap', url: '/', status: true, logo: true},
                {title: 'Screener', url: '/screener', status: true},
                {title: 'Market', url: '/market', status: true},
                {title: 'Features', url: '/features', status: true}
            ]
        }
    }
}
</script>

<style scoped>
</style>

<template>
    <b-navbar type="dark" toggleable="lg" v-bind:sticky="true" id="nav">
        <b-navbar-brand>
            <img v-if="this.$site.themeConfig.preferences.avatar != null" :src="this.$site.themeConfig.preferences.avatar" class="avatar"/>
            <h1 class="title">{{ title }}</h1>
        </b-navbar-brand>
        <b-navbar-toggle target="collapse"></b-navbar-toggle>
        <b-collapse id="collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item-dropdown text="Feed" v-if="this.$service.feed.rss || this.$service.feed.atom || this.$service.feed.json">
                    <b-dropdown-item :href="this.$site.base+'rss.xml'" v-if="this.$service.feed.rss">RSS</b-dropdown-item>
                    <b-dropdown-item :href="this.$site.base+'feed.atom'" v-if="this.$service.feed.atom">Atom</b-dropdown-item>
                    <b-dropdown-item :href="this.$site.base+'feed.json'" v-if="this.$service.feed.json">JSON</b-dropdown-item>
                </b-nav-item-dropdown>
                <b-nav-item :href="this.$site.base">Home</b-nav-item>
                <b-nav-item :href="this.$site.base+'tag/'">Tags</b-nav-item>
            </b-navbar-nav>
            <b-navbar-nav class="ml-auto">
                <b-nav-item v-for="link in this.$site.themeConfig.preferences.navlinks" :href="link.href">{{ link.title }}</b-nav-item>
            </b-navbar-nav>
        </b-collapse>
    </b-navbar>
</template>
<script>
export default {
    computed: {
        title() {
            if(!this.$page.path)return "404 Not Found";
            if(this.$page.frontmatter.title)return this.$page.frontmatter.title;
            return this.$page.title;
        }
    }
}
</script>
<style>
#nav{
    background-color: #563d7c;
    margin-bottom: 2rem;
    box-shadow: 0 0.25rem 0.25rem rgba(0,0,0,.25), inset 0 -1px 5px rgba(0,0,0,.25);
    line-height: 32px;
    user-select: none;
}
.avatar{
    width: 30px;
    height: 30px;
}
.title{
    font-size: 1.25rem;
    padding-left: .5em;
    display: inline;
}
</style>
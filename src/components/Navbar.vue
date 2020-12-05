<template>
    <div>
        <b-navbar toggleable="lg" type="dark" class="fixed-top shadow mynavbar">
            <b-navbar-brand href="/">Covid Tracker</b-navbar-brand>
            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <span class="text-danger"><a href="https://github.com/zh6ziq" target="_blank" class="a">@zh6ziq</a></span>
            </b-navbar-nav>
        </b-navbar>
    </div>  
</template>

<script>
export default {
    
}
</script>

<style scoped>
.mynavbar{
    background-color:rgba(94, 50, 252, 0.815);
}
.a{
    color: rgb(255, 153, 0)!important;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
</style>
<template>
    <div class="card shadow rounded mycard">
        <div class="card-body shadow rounded">
            <h3 class="card-title">{{ title }}</h3>
            <h4 class="card-text" v-if="value1">New: {{ value1 }}</h4>
            
            <h4 class="card-text">Total: {{ value2 }}</h4>
        </div>
    </div>
</template>

<script>

export default {
    props: {
        title: String,
        value1: String,
        value2: Number
    }
    
}
</script>

<style scoped>
.mycard{
    height: 150px;
}
</style>
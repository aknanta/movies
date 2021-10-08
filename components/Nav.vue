<template>
    <div class="topnav">
        <ul>
            <li><NuxtLink :to="{name: 'index'}" class="logo"> NetFlex</NuxtLink></li>
            <li><NuxtLink to="serial-tv">Serial Tv</NuxtLink></li>
        </ul>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
    .topnav{
        height: 50px;
        width:100%;
        li{
        color: white;
        display: inline-block;
        padding: 10px;
        a{
            text-decoration: none;
            color: white;
        }
        
    }
    .logo{
        top: 0;
        left: 0;
        padding: 10px;
        color: #c92502;
    }
    }
</style>
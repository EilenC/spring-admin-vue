<template>
    <div>
        <div id="container" style="width: 100%; height: calc(100vh - 100px)"></div>
    </div>
</template>

<script>
export default {
    name: "Map",
    data() {
        return {}
    },
    created() {

    },
    mounted() {
        // 创建地图实例
        var map = new AMap.Map("container", {
            zoom: 12,
            // center: [116.396901,39.919544],
            resizeEnable: true
        })
    },
    methods: {}
}
</script>

<style>

</style>

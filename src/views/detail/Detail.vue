<template>
    <div>
        <h2>详情页</h2>
        {{iid}}
    </div>
    
</template>

<script>
export default {
    name:"Detail",
    data() {
        return {
            iid:null
        }
    },
    created() {
        this.iid = this.$route.params.iid
    }
}
</script>

<style scoped>

</style>
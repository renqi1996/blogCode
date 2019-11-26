<template>
    <div style="display: flex;flex-wrap: wrap;">
        <el-card shadow="hover" v-for="item in data" :key="item.domain" @click.native="goto(item.domain)" style="width: 30%;margin-bottom: 1rem;margin-right: 1rem;text-align: center;border: none;">
          {{item.name}}
        </el-card>
    </div>
</template>

<script>
export default {
    data() {
        return {
       
        }
    },
    props: {
      data: {
        type: Array,
        defaul: () => []
      }
    },
    methods: {
      goto (page) {
        window.open(page, '_blank')
      }
    },
    created () {
      console.log(this.data)
    }
}
</script>


<style scoped>
.el-card.is-always-shadow, .el-card.is-hover-shadow:focus, .el-card.is-hover-shadow:hover {
    box-shadow: 0 2px 12px 0 rgba(0,0,0,.5);
}
.el-card:hover {
  cursor: default;
}
</style>
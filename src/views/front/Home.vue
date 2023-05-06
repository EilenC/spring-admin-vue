<template>
  <div>
    <div style="margin: 10px 0">
      <el-carousel height="450px;" :interval="10000">
        <el-carousel-item v-for="item in imgs" :key="item">
          <img :src="item" alt="" style="width: 100%">
        </el-carousel-item>
      </el-carousel>
    </div>

    <div style="margin: 10px 0">
      <el-row :gutter="10">
        <el-col :span="6" v-for="item in files" :key="item.id" style="margin-bottom: 10px">

          <div style="border: 1px solid #ccc; padding-bottom: 10px">
            <img :src="item.url" style="width: 100%; overflow: hidden;">
            <div style="color: #666; padding: 10px;overflow: hidden">{{ item.name }}</div>
            <div style="padding: 10px"><el-button type="primary">查看</el-button></div>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "FrontHome",
  data() {
    return {
      imgs: [
          // '../../assets/arch-linux-4k-mj-1366x768.jpg',
          // '../../assets/abstract-google-loading-4k-pa-1336x768.jpg',
          'https://imgcps.jd.com/ling-cubic/ling4/lab/amZzL3QxLzE0NzA1Mi83LzMyNjE4LzQxMDQzLzYzZTBiY2M1RjI2OTBjN2Q3Lzg3MDAzMmRkOTZiOGNlMzMucG5n/5Lqs6YCJ5aW96LSn/5L2g5YC85b6X5oul5pyJ/1635189098729897986/cr/s/q.jpg',
          'https://imgcps.jd.com/ling-cubic/ling4/lab/amZzL3QxLzE4Njg1Ni8xMS80NTY5LzQxNTUwNy82MGFhNWRmYUU1YmUwOGQ4OS9iMzg1OWMxOGFkN2JhOGYxLnBuZw/5Lqs6YCJ5aW96LSn/5L2g5YC85b6X5oul5pyJ/1635183047968657409/cr/s/q.jpg'
      ],
      files: []
    }
  },
  created() {
    this.request.get("/echarts/file/front/all").then(res => {
      console.log(res.data)
      this.files = res.data.filter(v => v.type === 'png' || v.type === 'jpg' || v.type === 'webp' || v.type === 'gif')
    })
  },
  methods: {

  }
}
</script>

<style>

</style>

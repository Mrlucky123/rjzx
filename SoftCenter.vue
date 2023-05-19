<template>
  <div id="app" style="overflow-x: hidden">
    <el-container style="width: 882px; height: 450px">
      <el-header>
        <el-row type="flex" justify="center" align="middle">
          <el-col :span="12">
            <h1>软件中心</h1>
          </el-col>
          <el-col :span="12">
            <el-input
              v-model="query"
              placeholder="请输入软件名称"
              prefix-icon="el-icon-search"
              @keyup.enter.native="search"
            ></el-input>
          </el-col>
        </el-row>
      </el-header>
      <el-main>
        <el-row type="flex" justify="center" align="middle">
          <el-col :span="24">
            <el-menu
              mode="horizontal"
              default-active="1"
              class="el-menu-horizontal-demo"
              @select="selectCategory"
            >
              <el-menu-item index="1">全部</el-menu-item>
              <el-menu-item index="2">办公</el-menu-item>
              <el-menu-item index="3">游戏</el-menu-item>
              <el-menu-item index="4">音乐</el-menu-item>
              <el-menu-item index="5">视频</el-menu-item>
              <el-menu-item index="6">工具</el-menu-item>
            </el-menu>
          </el-col>
        </el-row>
        <div class="software-list">
          <div
            class="software-card"
            v-for="(software, index) in filteredSoftwareList"
            :key="index"
          >
            <img :src="software.icon" alt="" />
            <div class="software-info">
              <h3>{{ software.name }}</h3>
              <p>{{ software.description }}</p>
              <p>{{ software.size }} MB</p>

              <button @click="download(software)">下载</button>
            </div>
          </div>
        </div>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      query: "",
      category: "全部",
      softwareList: [
        {
          name: "Word",
          icon: "https://cdn.iconscout.com/icon/free/png-256/microsoft-word-2-569282.png",
          description: "创建、编辑和共享文档",
          size: 200,
          rating: 4.5,
        },
        {
          name: "Excel",
          icon: "https://cdn.iconscout.com/icon/free/png-256/microsoft-excel-2-569277.png",
          description: "处理数据和制作图表",
          size: 180,
          rating: 4.2,
        },
        {
          name: "PowerPoint",
          icon: "https://cdn.iconscout.com/icon/free/png-256/microsoft-powerpoint-2-569280.png",
          description: "制作演示文稿和幻灯片",
          size: 150,
          rating: 4.0,
        },
        {
          name: "Angry Birds",
          icon: "https://cdn.iconscout.com/icon/free/png-256/angry-birds-225998.png",
          description: "用弹弓发射小鸟，击落小猪",
          size: 50,
          rating: 4.8,
        },
        {
          name: "Spotify",
          icon: "https://cdn.iconscout.com/icon/free/png-256/spotify-11-432546.png",
          description: "听你喜欢的音乐和播客",
          size: 40,
          rating: 4.6,
        },
        {
          name: "YouTube",
          icon: "https://cdn.iconscout.com/icon/free/png-256/youtube-85-226402.png",
          description: "观看和分享视频",
          size: 60,
          rating: 4.7,
        },
        {
          name: "Photoshop",
          icon: "https://cdn.iconscout.com/icon/free/png-256/adobe-photoshop-2-226055.png",
          description: "编辑和处理图片",
          size: 300,
          rating: 4.9,
        },
        {
          name: "WinRAR",
          icon: "https://cdn.iconscout.com/icon/free/png-256/winrar-3-569289.png",
          description: "压缩和解压缩文件",
          size: 10,
          rating: 4.3,
        },
      ],
    };
  },
  computed: {
    filteredSoftwareList() {
      return this.softwareList.filter(
        (software) =>
          (this.category === "全部" ||
            software.name
              .toLowerCase()
              .includes(this.category.toLowerCase())) &&
          (this.query === "" ||
            software.name.toLowerCase().includes(this.query.toLowerCase()))
      );
    },
  },
  methods: {
    search() {
      console.log("Searching for", this.query);
    },
    selectCategory(index) {
      this.category = index === "1" ? "全部" : index;
      console.log("Selecting category", this.category);
    },
    download(software) {
      console.log("Downloading", software.name);
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
h1 {
  color: #409eff;
}
.software-list {
  display: flex;
}
.software-card {
  margin: 10px;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.1) -1px -1px inset,
    rgba(0, 0, 0, 0.1) -1px -1px inset, rgba(0, 0, 0, 0.1) -1px -1px inset;
}
.software-card img {
  width: 200px;
  height: 200px;
}
.software-info {
  padding-left: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.software-info h3 {
  font-size: 20px;
  font-weight: bold;
}
.software-info p {
  font-size: 14px;
  color: #666666;
}
.software-info button {
  width: 80px;
  height: 30px;
  border-radius: 5px;
  background-color: #409eff;
  color: white;
  border: none;
}
</style>


<!--
@Author: 左盐
@Date:   2018-03-05 16:18:21
@Email:  huabinglan@163.com
@Last modified by:   左盐
@Last modified time: 2018-03-31 10:10:13
-->



<style lang="less">
.title {
  height: 30px;
  line-height: 30px;
  margin-top: 30px;
  margin-bottom: 10px;
}
</style>
<template>
  <div id="app" style="width:1000px;margin:100px auto;">
    <h2 class="title">alert</h2>
    <el-button type="primary" @click="submitHandle">提交</el-button>
    <h2 class="title">confirm</h2>
    <el-button type="primary" @click="confirmHandle">删除</el-button>
    <h2 class="title">msg</h2>
    <el-button type="primary" @click="msgHandle">msg</el-button>
    <el-button type="primary" @click="msg1Handle">带回调</el-button>
    <h2 class="title">loading</h2>
    <el-button type="primary" @click="loadingHandle">默认样式</el-button>
    <h2 class="title">prompt</h2>
    <el-button type="primary" @click="promptHandle">弹出</el-button>
    <h2 class="title">tips</h2>
    <el-button type="primary" id="tips" @click="tipsHandle">上</el-button>
    <el-button type="primary" id="tips1" @mouseenter.native="tips1Handle">右</el-button>
    <el-button type="primary" id="tips2" @click="tips2Handle">下</el-button>
    <el-button type="primary" id="tips3" @click="tips3Handle">左-自定义样式</el-button>
    <h2 class="title">page</h2>
    <el-button type="primary" id="tips" @click="pageHandle">自定义</el-button>
    <br>
    <br>
    <br>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column label="日期" width="180">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{ scope.row.date }}</span>
        </template>
      </el-table-column>
      <el-table-column label="姓名" width="180">
        <template slot-scope="scope">
          <el-popover trigger="hover" placement="top">
            <p>姓名: {{ scope.row.name }}</p>
            <p>住址: {{ scope.row.address }}</p>
            <div slot="reference" class="name-wrapper">
              <el-tag size="medium">{{ scope.row.name }}</el-tag>
            </div>
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="submitHandle(scope.$index, scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="confirmHandle(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import tools from "./js/tools.js";
import formComp from "./form.vue";

export default {
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄"
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄"
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄"
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄"
        }
      ]
    };
  },
  components: {
    "base-form": formComp
  },
  async mounted() {
    let ids = [];
    for (let i = 0; i < 5; i++) {
      await tools.sleep(10);
      let id = this.loadingHandle();
      ids.push(id);
    }
    for (let i = 0; i < 5; i++) {
      await tools.sleep(200);
      this.$layer.close(ids[i]);
    }
    this.$on("asd", function(val) {
      this.$layer.msg(val);
    });
  },
  methods: {
    submitHandle: function() {
      this.$layer.alert(
        "this is demo!!!<br/>this is demo!!!<br/>this is demo!!!<br/>this is demo!!!<br/>this is demo!!!<br/>this is demo!!!<br/>this is demo!!!<br/>this is demo!!!this is demo!!!this is demo!!!this is demo!!!this is demo!!!this is demo!!!this is demo!!!this is demo!!!this is demo!!!",
        {
          shade: true
        },
        index => {
          this.$layer.close(index);
        }
      );
    },
    confirmHandle: function() {
      let id = this.$layer.confirm(
        "确定要<br/>删除吗？",
        {
          btn: ["asd", "4545"]
        },
        () => {
          this.$layer.msg("执行了删除");
          this.$layer.close(id);
        },
        () => {
          this.$layer.msg("执行取消");
          this.$layer.close(id);
        }
      );
    },
    msgHandle: function() {
      let id = this.$layer.msg("弱弱的提示");
    },
    msg1Handle: function() {
      let id = this.$layer.msg(
        "5s后刷新页面",
        {
          time: 5
        },
        () => {
          this.$layer.close(id);
        }
      );
    },
    loadingHandle: function() {
      let id = this.$layer.loading({
        time: 3
      });
      return id;
    },
    promptHandle: function() {
      this.$layer.prompt("你好");
    },
    tipsHandle: function() {
      let id = this.$layer.tips("在很久很久以前", "#tips", {
        tips: 0,
        time: 100
      });
    },
    tips1Handle: function() {
      let id = this.$layer.tips(
        "在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，",
        "#tips1",
        {
          tips: 1,
          time: 100
        }
      );
    },
    tips2Handle: function() {
      let id = this.$layer.tips(
        "在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，",
        "#tips2",
        {
          tips: 2
        }
      );
    },
    tips3Handle: function() {
      let id = this.$layer.tips(
        "在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，在很久很久以前，",
        "#tips3",
        {
          tips: [
            3,
            {
              selfa: true
            }
          ],
          time: 10
        }
      );
    },
    pageHandle: function() {
      let ids = this.$layer.iframe({
        content: {
          content: formComp,
          parent: this,
          data: {
            check: "aaaaaaaaxxxx",
            fn: function() {
              alert(1);
            }
          }
        },
        area: ["900px", "600px"],
        title: "",
        shade: false
      });
    }
  }
};
</script>

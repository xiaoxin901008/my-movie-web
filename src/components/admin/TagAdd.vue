<template>
  <div class="main">
    <div class="main-title1">
      <Breadcrumb>
        <a @click="goBack" class="back">
          <Icon type="md-return-left" size="16"/>
        </a>
        <BreadcrumbItem to="/admin/tag">标签管理</BreadcrumbItem>
        <BreadcrumbItem>添加标签</BreadcrumbItem>
      </Breadcrumb>
    </div>
    <div style="background: #fff;
    box-shadow: 0 0 18px 1px #ccc;
    border-radius: 3px;
    margin-top: 15px;">
      <Card :bordered="false" dis-hover>
        <p slot="title">添加标签</p>
        <p style="margin-bottom: 5px;">标签名称</p>
        <Input v-model="name" placeholder="请输入标签名称..." clearable style="width: 100%" />
      </Card>
      <Divider />
      <div style="padding: 0 0 15px 10px">
        <Button type="default" size="large" @click="goBack">取消</Button>
        <Button type="primary" size="large" @click="add">添加</Button>
      </div>
    </div>

  </div>

</template>

<script>
  import {addTag} from '../../api/index.js';
  export default {
    created() {
    },
    data() {
      return {
        /*  添加标签属性 */
        name: null,          // 机房名称

      }
    },
    computed: {},
    components: {},
    methods: {
      // 返回上一级页面
      goBack() {
        this.$router.go(-1)
      },

      // 添加标签
      async add() {
        if (this.name === null) {
          this.$Message.warning('请输入标签名称');
          return
        }
        let json_data = {
          name: this.name,
        };
        //  标签添加成功后，应当将添加成功的ID返回，然后追加到列表中，添加完成后，初始化模态框信息         // 否则为新建
        let resp = await addTag(json_data);
        if (resp.state === 1) {
          this.$Message.success('标签添加成功');
          this.name = null;
        } else if (resp.state === 2) {
          this.$Message.warning('添加失败，标签已存在')
        } else {
          this.$Message.success('标签添加失败');
        }
    },
    },
  }
</script>

<style>

</style>



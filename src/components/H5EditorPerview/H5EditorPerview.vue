<template>
  <el-dialog
      title="预览效果"
      :center="true"
      :visible.sync="dialogVisible"
      :modal-append-to-body="false"
      :append-to-body="true"
      width="327px">
    <div class="previewmobile">
      <div class="previewmobile-bg">
        <img :src="require('@/images/H5Editor/iphone_bg.png')" alt="">
      </div>
      <div class="mobileheader">模板</div>
      <div class="mobileview"
           :style="{
              width: viewBg.width + 'px',
              height: viewBg.height + 'px',
              backgroundColor: viewBg.backgroundColor,
              backgroundImage: viewBg.backgroundImage,
           }">
        <div class="mobileitem"
             :style="{
                        left: item.x + 'px',
                        top: item.y + 'px',
                        width: item.w + 'px',
                        height: item.h + 'px',
                        zIndex: item.zIndex
                      }"
             v-for="(item, idx) in layoutList" :key="idx">
          {{ item }}
        </div>
      </div>
    </div>
    <span slot="footer" class="dialog-footer">
    <el-button type="primary" @click="dialogVisible = false">提 交</el-button>
  </span>
  </el-dialog>
</template>

<script>
const previewWidth = 225
const previewHeight = 444
const originWidth = 375
const originHeight = 667
import _ from 'lodash'
export default {
    name: 'H5EditorPerview',
    props: {
        componentList: [],
        bgItem: Object
    },
    computed: {
        layoutList () {
            let list = []
            list = this.componentList.map(item => {
                let obj = _.cloneDeep(item)
                obj.x = parseInt((obj.x * previewWidth) / originWidth)
                obj.y = parseInt((obj.y * previewHeight) / originHeight)
                obj.w = parseInt((obj.w * previewWidth) / originWidth)
                obj.h = parseInt((obj.h * previewHeight) / originHeight)
                return obj
            })
            return list
        },
        viewBg () {
            let obj = _.cloneDeep(this.bgItem.style)
            obj.width = previewWidth
            obj.height = parseInt((obj.height * previewHeight) / originHeight)
            return obj
        }
    },
    data () {
        return {
            dialogVisible: false
        }
    },
    methods: {
        openDialog () {
            this.dialogVisible = true
        }
    }
}
</script>

<style lang="scss" scoped>
.previewmobile{
  display: flex;
  flex-direction: column;
  width: 236px;
  height: 498px;
  margin: 0 auto;
  position: relative;
  //background: url("../../images/H5Editor/iphone_bg.png") center center no-repeat;
  //background-size: cover;
  &-bg{
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    z-index: 2;
    img{
      width: 100%;
      height: 100%;
      overflow: hidden;
    }
  }
  .mobileheader{
    flex: 0 0 54px;
    height: 54px;
    line-height: 54px;
    text-align: center;
  }
  .mobileview{
    flex: 1;
    position: relative;
    margin: 0 auto 6px auto;
  }
  .mobileitem{
    position: absolute;
    display: inline-block;
    touch-action: none;
    transform: translate(0px, 0px);
    transition: background-color 0.3s;
    border: 0.8px dashed #ddd;
    box-sizing: border-box;
    border-radius: 4px;
    overflow: auto;
    &-content{
      width: 100%;
      height: 100%;
      position: relative;
    }
  }
}
</style>

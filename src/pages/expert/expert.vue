<template>
  <div class="container">
    <wux-row>
        <wux-col span="8" offset="4">
            <div style="font-size:64rpx">专家认证</div>
        </wux-col>
    </wux-row>
    <wux-white-space body-style="height: 30rpx" />
    <wux-row>
        <wux-col span="10" offset="1">
            <wux-cell hover-class="none">
                <wux-input clear label="真实姓名" placeholder="请输入您的真实姓名" />
            </wux-cell>
        </wux-col>
        <wux-col span="10" offset="1">
            <wux-cell hover-class="none">
                <wux-input clear label="身份证号" placeholder="请输入您的身份证号" />
            </wux-cell>
        </wux-col>
        <wux-col span="10" offset="1">
            <wux-select id="wux-select1" />
              <wux-cell title="认证领域" :extra="title1"  @click="onClick"></wux-cell>
            <wux-cell hover-class="none">
                <wux-input clear label="认证领域" placeholder="请输入您的身份证号" />
            </wux-cell>
        </wux-col>
        <wux-col span="10" offset="1">
            <view class="sub-title"></view>
                 <wux-upload url="https://www.skyvow.cn/api/common/file" bind:change="onChange" bind:success="onSuccess"
                  bind:fail="onFail" bind:complete="onComplete">
            <button type="default">点此上传您的证明材料</button>
        </wux-upload>
        </wux-col>
    </wux-row>
    <wux-row>
        <wux-white-space body-style="height: 30rpx" />
        <wux-col span="10" offset="2">
            <wux-upload listType="picture-card" :defaultFileList="fileList" max="6" 
                url="https://www.skyvow.cn/api/common/file" @change="onChange" @success="onSuccess"
                @fail="onFail" @complete="onComplete" @preview="onPreview" @remove="onRemove">
                <text style="font-size:30rpx" >上传材料</text>
            </wux-upload>            
        </wux-col>  
    </wux-row>
    <view class="expert">
        <wux-row>
            <wux-col span="8" offset="2">
                <wux-button block type="positive" >点击认证</wux-button>
            </wux-col>     
        </wux-row>   
    </view>
  </div>
</template>

<script>
import { $wuxSelect } from '../../../static/wux-ui/index'
export default {
  data () {
    return {
       imageUrl:'',
       title1: '',
    }
  },

  methods: {
    onClick() {
        var that=this;
        $wuxSelect('#wux-select1').open({
            options: [
                '粮油',
                    '茶叶',
                    '花卉',
                    '水产',
                    '畜牧',
                    '水果',
                    '蔬菜',
                    '桑蚕',
                    '食用菌',
                    '中药材',
                    '饲料',
                    '兽医',
                    '植保',
                    '植检',
                    '土壤',
                    '肥料',
                    '种子',
                    '生态',
                    '农机',
             ],
             onConfirm: (value, index, options) => {
                if (index !== -1) {
                   that.title1 = options[index];    
                 }
             },
        })
    },
    onChange(e) {
        console.log('onChange', e)
        const file  = e.target.file
        if (file.status === 'uploading') {
            wx.showLoading()
        } 
        else if (file.status === 'done') {
            this.imageUrl=file.url;
        }
    },
    onSuccess(e) {
        console.log('onSuccess', e)
    },
    onFail(e) {
        console.log('onFail', e)
    },
    onComplete(e) {
        console.log('onComplete', e)
        wx.hideLoading()
    },
    onPreview(e) {
        console.log('onPreview', e)
        const file=e.detail
        const fileList = e.detail
        wx.previewImage({
            current: file.url,
            urls: fileList.map((n) => n.url),
        })
    },
    onRemove(e) {
        console.log('onRemove', e)
        const file=e.detail
        const fileList = e.detail
        wx.showModal({
            content: '确定删除？',
            success: (res) => {
                console.log('success');
            },
        })
    },

  }
}
</script>

<style scoped>

</style>
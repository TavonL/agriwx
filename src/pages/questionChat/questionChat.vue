<template>
  <div class="container" >
    <view class="timeline">
    <scroll-view scroll-y scroll-into-view='item2'>
    <wux-row>
        <wux-col span="11" offset="1">
          <div class="message" v-for="item in timeAxis1">
            <div class="circle"><img src="../../../static/images/circle2.png" alt=""></div><span class="time">{{item.time}}</span>
            <div class="lineborder">
              <img src="../../../static/images/farm.jpg">
                 <div class="blueBorder">
                    <div class="blueRadius">
                    </div>
                    <div class="blueRadius">
                   </div>
                 </div>
            </div>
          </div>
        </wux-col>
    </wux-row>
    </scroll-view>
    </view>
    <view class="Input">
    <wux-row>
      <wux-col span="12">
            <wux-cell-group>
               <wux-cell hover-class="none">
                   <wux-textarea hasCount rows="3" cursorSpacing="80" placeholder="在这儿回复..." />
               </wux-cell>
            </wux-cell-group>
      </wux-col>
    </wux-row>
    <wux-white-space body-style="height: 20rpx" />
    <wux-row>
      <wux-col span="8" offset="1">
            <wux-upload listType="picture-card" :defaultFileList="fileList" max="2" 
                url="https://www.skyvow.cn/api/common/file" @change="onChange" @success="onSuccess"
                @fail="onFail" @complete="onComplete" @preview="onPreview" @remove="onRemove">
            <text style="font-size:30rpx">上传图片</text>
          </wux-upload>            
      </wux-col> 
      <wux-col span="2">
        <wux-button block type="balanced" size="small" >提交</wux-button>
      </wux-col>
    </wux-row>
    </view>
    <wux-white-space body-style="height: 20rpx" />
  </div>
</template>

<script>
export default {
  data () { 
    return {
      timeAxis1: [
          {time: '2019年2月10日'},
          {time: '2019年2月16日'},
          {time: '2019年2月21日'},
          {time: '2019年2月27日'}
      ],
    }
  },

  methods: {
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
.timeline scroll-view{
    height: 800rpx;
}
.message{
    display: inline-block;
    width: 100%;
    height: 450rpx;
  }
  .circle{
    margin-left: 35rpx;
    margin-right: 50rpx;
    display: inline-block;
    height: 40rpx;
    width: 40rpx;
    float: left;
  }
  .lineborder{
    margin-left: 50rpx;
    display: inline-block;
    height: auto;
    width: 100%;
    left: 200rpx;
    border-left: 5rpx solid #999999;
  }
  .lineborder img{
    display: inline-block;
    width: 500rpx;
    height: 300rpx;
    margin-left:75rpx;
    margin-top:15rpx;
    margin-bottom: 15rpx;
  }
  .lineborder p{
    border-width: medium;
    border-color:#4D8AD7; 
    margin-left:80rpx ;
  }
  .circle img{
    max-width:100%;
    max-height:100%;
  }
  .blueBorder{
  display: inline-block;
  margin-left:75rpx ;
  width: 500rpx;
  height: 300rpx;
  border:4rpx solid rgba(63,174,174,1);
  border-radius: 40rpx;
  position: relative;
}
.blueBorder div{
  display: inline-block;
  position: absolute;
}
.blueRadius{
  display: inline-block;
  width: 24rpx;
  height: 24rpx;
  border-radius: 12rpx;
  background-color: rgba(63,174,174,1);
}

</style>
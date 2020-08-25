<template>
  <view class="container">
    <iv-list v-for="(item,index) in listNews" :key="index">
      <iv-list-chat
        :avatar-circle="true"
        :title="item.newsTitle"
        :clickable="true"
        :avatar="item.state==1? avatar1 : avatar2"
        :note="item.newsNote"
        :time="item.newsTime"
        @click="onClick(item.state)"
      ></iv-list-chat>
    </iv-list>
  </view>
</template>
<script>
import ivList from "@/components/uni-list/uni-list.vue";
import ivListChat from "@/components/uni-list-chat/uni-list-chat.vue";
export default {
  components: { ivList, ivListChat },
  data() {
    return {
      avatar1: "../../static/images/xi.png",
      avatar2: "../../static/images/xi2.png",
      listNews: [
        {
          state: "1",
          newsTitle: "未读",
          newsTime: "2020-08-25 14:00",
          newsNote: "您收到一条新的消息",
        },
        {
          state: "0",
          newsTitle: "已读",
          newsTime: "2020-08-25 14:00",
          newsNote: "您收到一条新的消息",
        },
        {
          state: "1",
          newsTitle: "未读",
          newsTime: "2020-08-25 14:00",
          newsNote: "您收到一条新的消息",
        },
      ],
    };
  },
  methods: {
    onClick(type) {
      if (type == 0) {
        console.log("点击了一个已读消息");
        return false;
      } else {
        console.log("点击了未读消息");
        return false;

      }
    },
  },
};
</script>
<style scoped>
.chat-custom-right {
  flex: 1;
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
}

.chat-custom-text {
  font-size: 12px;
  color: #999;
}
</style>
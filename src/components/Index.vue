<template>
  <table class="list-table">
    <thead>
      <tr class="list-table-title">
        <th>会议标题</th>
        <th>发起人</th>
        <th>地点</th>
        <th>日期</th>
      </tr>
    </thead>

    <tbody>
      <template v-for="meeting in meetingLits">
        <tr>
          <td>{{ meeting.name }}</td>
          <td>{{ meeting.user.username }}</td>
          <td>{{ meeting.location }}</td>
          <td>{{ meeting.start_time }}</td>
        </tr>
      </template>
    </tbody>
  </table>
</template>

<script>
import axios from 'axios';
import { Toast } from 'mint-ui';

export default {
  name: 'index',
  created() {
    axios.get(`${process.env.BASE_URL}/meeting/findList`)
    .then((response) => {
      if (response.status === 200) {
        if (response.data.code === 200) {
          this.meetingLits = response.data.data;
        } else {
          Toast({
            message: response.data.message,
            duration: 1500,
          });
        }
      }
    }).catch((err) => {
      Toast({
        message: err.message,
        duration: 1500,
      });
    });
  },
  data() {
    return {
      meetingLits: [],
    };
  },
  methods: {

  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list-table {
  background-color: #fff;
  line-height: 40px;
  position: relative;
  width: 100%;
  border-collapse: collapse;
}

.list-table::after {
  content: " ";
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  height: 1px;
  border-top: 1px solid #C7C7C7;
  color: #C7C7C7;
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
  -webkit-transform: scaleY(0.5);
  transform: scaleY(0.5);
}

.list-table th {
  font-weight: 500;
}

.list-table td, .list-table th {
  position: relative;
  border-right: 0;
  border-left: 0;
  text-align: center;
}

.list-table td:before, .list-table th:before {
  content: " ";
  position: absolute;
  left: 0;
  bottom: 0;
  right: 0;
  height: 1px;
  border-bottom: 1px solid #C7C7C7;
  color: #C7C7C7;
  -webkit-transform-origin: 0 100%;
  transform-origin: 0 100%;
  -webkit-transform: scaleY(0.5);
  transform: scaleY(0.5);
}

.list-table td:after, .list-table th:after {
  content: " ";
  position: absolute;
  right: 0;
  top: 0;
  width: 1px;
  bottom: 0;
  border-right: 1px solid #C7C7C7;
  color: #C7C7C7;
  -webkit-transform-origin: 100% 0;
  transform-origin: 100% 0;
  -webkit-transform: scaleX(0.5);
  transform: scaleX(0.5);
  border-right-width: 0;
}

.list-table-title {
  background-color: #f7f7f7;
}
</style>

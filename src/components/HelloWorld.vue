<template>
  <div class="con">
    <div class="header"><h1>Web Management Platform</h1></div><br><br>
    <div v-for="data of status" class="UI" v-if="data.indexOID !== 25 && data.indexOID !== 26 && data.indexOID !== 27 && data.indexOID < 7">
     <div class="led-yellow" v-if="data.intStatus === 1"></div>
     <div class="led-red" v-else></div>
     <br>
      <table>
        <tr>
          <td><button @click="sendData(data.indexOID, data.intStatus)" id="BB">{{data.indexOID}}</button></td>
        </tr>
      </table>
    </div>
    <span style="margin-right:40px;"></span>
    <div v-for="data of status" class="UI" v-if="data.indexOID !== 25 && data.indexOID !== 26 && data.indexOID !== 27 && data.indexOID > 6 && data.indexOID < 13">
    <div class="led-yellow" v-if="data.intStatus === 1"></div>
    <div class="led-red" v-else></div>
    <br>
      <table>
        <tr>
          <td><button @click="sendData(data.indexOID, data.intStatus)" id="BB">{{data.indexOID}}</button></td>
        </tr>
      </table>
    </div><br><br>

    <div v-for="data of status" class="UI" v-if="data.indexOID !== 25 && data.indexOID !== 26 && data.indexOID !== 27 && data.indexOID > 12 && data.indexOID < 19">
      <table>
        <tr>
          <td><button @click="sendData(data.indexOID, data.intStatus)" id="AA">{{data.indexOID}}</button></td>
        </tr>
      </table><br>
      <div class="led-yellow" v-if="data.intStatus === 1"></div>
      <div class="led-red" v-else></div>
    </div>
    <span style="margin-right:40px;"></span>
    <div v-for="data of status" class="UI" v-if="data.indexOID !== 25 && data.indexOID !== 26 && data.indexOID !== 27 && data.indexOID > 18">
      <table>
        <tr>
          <td><button @click="sendData(data.indexOID, data.intStatus)" id="AA">{{data.indexOID}}</button></td>
        </tr>
      </table><br>
      <div class="led-yellow" v-if="data.intStatus === 1"></div>
      <div class="led-red" v-else></div>
    </div><br><br><br><br><br><br>
    <div class="up">
      <button></button>
      <a style="color:black;font-weight:bold;">Port Up</a><br><br>
      <button style="background-color: #F00;"></button>
      <a style="color:black;font-weight:bold;">Port Down</a>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
var ax = axios.create({baseURL: 'http://192.168.1.19:3000'})

export default {
  name: 'HelloWorld',
  data () {
    return {
      datas: '',
      num: '',
      status: ''
    }
  },
  methods: {
    sendData (intName, intStatus) {
      console.log(intStatus)
      this.num = intName * 1
      if (intStatus === 1) {
        ax.post('/on', {'oidindex': intName, 'status': 'off'})
      } else {
        ax.post('/on', {'oidindex': intName, 'status': 'on'})
      }
      setTimeout(window.location.reload.bind(window.location), 2000)
    }
  },
  mounted () {
    ax.get('/intname').then((response) => {
      console.log(response.data)
      this.datas = response.data
    }).catch((error) => {
      console.log(error)
    })

    ax.get('/status').then((response) => {
      console.log(response.data)
      this.status = response.data
    }).catch((error) => {
      console.log(error)
    })
  }
}
</script>

<style scoped>
.con {
  margin: auto;
  width: 820px;
}
.up button {
  width: 50px;
  height: 50px;
  background-color: #ABFF00;
  border: 3px solid black;
  text-align: left;
}

button {
  width: 100%;
  height: 100%;
  cursor: pointer;
  text-decoration: none;
  border: none;
  background-color: #ffffff;
}

#AA {
  background-image:url('../assets/aaa.jpg/');
  background-size: 50px 50px;
  color: #ffffff;
}
#BB {
  background-image:url('../assets/bbb.png/');
  background-size: 50px 50px;
  color: #ffffff;
}
table {
  border: 3px solid black;
}
td {
  height: 50px;
  width: 50px;
}
.UI {
  display: inline-block;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.header {
  text-align: center;
}

.led-red {
  margin: 0 auto;
  width: 8px;
  height: 15px;
  background-color: #F00;
  box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 12px;
  -webkit-animation: blinkRed 0.3s infinite;
  -moz-animation: blinkRed 0.3s infinite;
  -ms-animation: blinkRed 0.3s infinite;
  -o-animation: blinkRed 0.3s infinite;
  animation: blinkRed 0.3s infinite;
}

@-webkit-keyframes blinkRed {
    from { background-color: #F00; }
    50% { background-color: #A00; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 0;}
    to { background-color: #F00; }
}
@-moz-keyframes blinkRed {
    from { background-color: #F00; }
    50% { background-color: #A00; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 0;}
    to { background-color: #F00; }
}
@-ms-keyframes blinkRed {
    from { background-color: #F00; }
    50% { background-color: #A00; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 0;}
    to { background-color: #F00; }
}
@-o-keyframes blinkRed {
    from { background-color: #F00; }
    50% { background-color: #A00; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 0;}
    to { background-color: #F00; }
}
@keyframes blinkRed {
    from { background-color: #F00; }
    50% { background-color: #A00; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #441313 0 -1px 9px, rgba(255, 0, 0, 0.5) 0 2px 0;}
    to { background-color: #F00; }
}

.led-yellow {
  margin: 0 auto;
  width: 8px;
  height: 15px;
  background-color: #ABFF00;
  box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 12px;
  -webkit-animation: blinkYellow 0.2s infinite;
  -moz-animation: blinkYellow 0.2s infinite;
  -ms-animation: blinkYellow 0.2s infinite;
  -o-animation: blinkYellow 0.2s infinite;
  animation: blinkYellow 0.2s infinite;
}

@-webkit-keyframes blinkYellow {
    from { background-color: #FF0; }
    50% { background-color: #AA0; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 0; }
    to { background-color: #FF0; }
}
@-moz-keyframes blinkYellow {
    from { background-color: #FF0; }
    50% { background-color: #AA0; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 0; }
    to { background-color: #FF0; }
}
@-ms-keyframes blinkYellow {
    from { background-color: #FF0; }
    50% { background-color: #AA0; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 0; }
    to { background-color: #FF0; }
}
@-o-keyframes blinkYellow {
    from { background-color: #FF0; }
    50% { background-color: #AA0; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 0; }
    to { background-color: #FF0; }
}
@keyframes blinkYellow {
    from { background-color: #FF0; }
    50% { background-color: #AA0; box-shadow: rgba(0, 0, 0, 0.2) 0 -1px 7px 1px, inset #808002 0 -1px 9px, #FF0 0 2px 0; }
    to { background-color: #FF0; }
}
</style>

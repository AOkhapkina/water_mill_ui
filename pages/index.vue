<template>
  <b-container style=" background: #2abd5b; text-align: center; justify-content: center;">
    <b-row>
      <b-col style="padding: 5%;">
        <ul class="tools">
          <li class="water" @click="addWater"><b-badge variant="primary">0</b-badge></li>
          <li class="txt">+</li>
          <li class="millet" @click="addMillet"><b-badge variant="warning"></b-badge></li>
          <li class="txt">=</li>
          <li class="flour" @click="dropFlour"><b-badge variant="primary"></b-badge></li>
        </ul>
        <div>
          <h3>Water: 0</h3>
          <b-progress :value="3" :max="10" animated variant="primary"></b-progress>
          <h3>Energy: 0</h3>
          <b-progress :value="4" :max="10" animated variant="warning"></b-progress>
          <h3>Millet: 0</h3>
          <b-progress :value="5" :max="10" animated variant="info"></b-progress>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import {mapGetters, mapActions} from "vuex"
export default {
  components: {},
  computed: mapGetters({
    state: "mill/getState" //ctrl + space
  }),
  //налаживаем связь с backend
  mounted(){
    this.socket = new WebSocket("ws://localhost:8080/websocket")
    this.socket.onopen =  ()=>{
      window.console.log("Socket opened")
    }
    this.socket.onmessage=(msg, ctx)=>{
      this.updateState(JSON.parse(msg.data)) // распарсить объект JSON
    }
    setInterval(this.pushSocket,300)
  },
  fetch(){
    this.$store.dispatch("mill/fetchData")
  },
  //Диспетчеризация действий в компонентах при помощи this.$store.dispatch('xxx')
  // или используя вспомогательную функцию mapActions, создающую локальные псевдонимы для действий
  // в виде методов компонента (требуется наличие корневого $store)
  methods: {
    pushSocket(){
      this.socket.send(new Date());
    },
    updateState(){
      this.$store.dispatch("mill/updateState", data)
    },
    addWater() {
      this.$store.dispatch("mill/addWater", 10)
    },
    addMillet() {
      this.$store.dispatch("mill/addMillet", 10)
    },
    dropFlour() {
      this.$store.dispatch("mill/dropFlour")
    }
  }
}
</script>



<style>
.tools {
  list-style: none;
  display: inline-flex;
}
.tools li {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: #35495e 3px solid;
}
.tools li.txt {
  border: none;
  line-height: 80px;
  color: #fff;
  font-size: 200%;
}
.tools li.water {
  background: #fff url(/water.png)  no-repeat center center/cover;
}
.tools li.millet {
  background: #fff url(/millet.png) no-repeat center center/cover;
}
.tools li.flour {
  background: #fff url(/flour.png) no-repeat center center/cover;
}
</style>

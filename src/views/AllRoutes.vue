<template>
  <div>
    <h3> All Route  </h3>
    <div id="table">
    <!-- Task 1 -->
    <table>
      <tr>
        <th>From</th>
        <th>To</th>
        <th>Cost</th>
        <th>Time</th>
        <th>Date</th>
      </tr>
      
      <tr v-for="r in this.routes" :key="r.id">
        <td>{{ r.fromcity }}</td>
        <td>{{ r.tocity }}</td>
        <td v-if="r.cost > 12" class="caro">{{ r.cost }}</td>
        <td v-else class="normal"> {{ r.cost }} </td>
        <td>{{ r.departuretime }}</td>
        <td>{{ r.departuredate }}</td>
      </tr>
    </table>
    </div>

    <footer>
      <span> We have {{ this.total }} trips today!</span>
    </footer>
  </div>
</template>


<script>
export default{
  name:"AllRoutes",
  data(){
    return{
      routes:[],
      total: 0
    }
  },
  methods:{
    fetchRoutes(){
      fetch("http://localhost:3000/api/routes")
      .then((response) => response.json())
      .then((data) => {
        this.routes = data;
        this.total = data.length
      })
      .catch((err) => console.log(err))
    }
  },
  mounted(){
    this.fetchRoutes()
    console.log("Mounted")
  }
}
</script>

<style scoped>
td{
  text-align: center;
  background-color: rgb(191, 212, 191);
  padding: 7px 10px;
}

th{
  text-align: center;
  background-color: rgb(106, 131, 106);
  padding: 7px 10px;
}

#table{
  display:flex;
  background-color:rgb(196, 196, 196);
  justify-content: center;
  align-content: center;
  padding: 20px;
}

.caro{
  background-color: rgb(255, 140, 140);
}

.normal{
  background-color: rgb(151, 151, 255);
}

footer{
  background-color: gray;
  padding: 20px;
}

footer span{
  font-size: 20px;
}

</style>
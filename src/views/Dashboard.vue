<template>
  <div class="py-4 container-fluid">
    <div class="row">
      <div class="col">
        <div id="mapLayer">
          <div id="point" style="position: absolute; top: 100px; left: 100px;">
            <img id="look-point" src="../assets/Polygon 1.png" width="60" alt="화각">
          </div>
          <img @click="test" class="mapimg" src="../assets/7403915272e_l.jpg" width="600" alt="한반도">
        </div>
      </div>
      <div class="col">
        <div class="card">
          <h5>1. 위치좌표 구하기 : e.offsetX,e.offsetY 사용</h5>

          <p>
          <h5>2. 좌표에 이미지 추가하기 : 그냥 네모 추가해서 부모로 함께 묶어줌</h5>
          'style="position: absolute; top: 100px; left: 100px;"'이걸 형식을 사용해서 <br />
          point.style.top = 0; 이런 식으로 바꿔줘야한다. 아니면 안바뀌고 에러 뜸
          </p>

          <h5>3. css transform을 이용해서 클릭시 원하는 각도만큼 회전하기</h5>


        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Card from "@/examples/Cards/Card.vue";
import ActiveUsersChart from "@/examples/Charts/ActiveUsersChart.vue";
import GradientLineChart from "@/examples/Charts/GradientLineChart.vue";
import OrdersCard from "./components/OrdersCard.vue";
import ProjectsCard from "./components/ProjectsCard.vue";
import US from "../assets/img/icons/flags/US.png";
import DE from "../assets/img/icons/flags/DE.png";
import GB from "../assets/img/icons/flags/GB.png";
import BR from "../assets/img/icons/flags/BR.png";

export default {
  name: "DashboardDefault",
  components: {
    Card,
    ActiveUsersChart,
    GradientLineChart,
    ProjectsCard,
    OrdersCard,
  },
  data() {
    return {
      stats: {
        iconBackground: "bg-gradient-success",
        money: {
          title: "Today's Money",
          value: "$53,000",
          percentage: "+55%",
          iconClass: "ni ni-money-coins",
        },
        users: {
          title: "Today's Users",
          value: "2,300",
          percentage: "+3%",
          iconClass: "ni ni-world",
        },
        clients: {
          title: "New Clients",
          value: "+3,462",
          percentage: "-2%",
          iconClass: "ni ni-paper-diploma",
          percentageColor: "text-danger",
        },
        sales: {
          title: "Sales",
          value: "$103,430",
          percentage: "+5%",
          iconClass: "ni ni-cart",
        },
      },
      sales: {
        us: {
          country: "United States",
          sales: 2500,
          value: "$230,900",
          bounce: "29.9%",
          flag: US,
        },
        germany: {
          country: "Germany",
          sales: "3.900",
          value: "$440,000",
          bounce: "40.22%",
          flag: DE,
        },
        britain: {
          country: "Great Britain",
          sales: "1.400",
          value: "$190,700",
          bounce: "23.44%",
          flag: GB,
        },
        brasil: {
          country: "Brasil",
          sales: "562",
          value: "$143,960",
          bounce: "32.14%",
          flag: BR,
        },
      },
    };
  },
  mounted() {
    // var layer = document.getElementById('mapLayer');
    // console.log(layer);
  },
  methods: {
    test(e) {
      // console.log(e);
      console.log(e.offsetX, e.offsetY);

      // point의 css를 직접 바꿔준다.
      const point = document.getElementById('point');
      point.style.top = e.offsetY.toString() + 'px';
      point.style.left = e.offsetX.toString() + 'px';
      // console.log(point.style.top, point.style.left);
    }
  }
};
</script>
<style>
#mapLayer {
  position: relative;
  display: block;
  width: 600px;
  height: 600px;
}

.mapimg {
  position: relative;
  display: block;
  /* margin: auto; */
}

#point {
  width: 10px;
  height: 10px;
  background: red;
  z-index: 9999;
}

#look-point {
  position: absolute;
  top: -84px;
  left: -24px;
  z-index: 9999;
  transition: all ease 1s;
}

#look-point:hover{
  top: -42px;
  left: 32px;
  transform: rotate( 90deg );
}
</style>
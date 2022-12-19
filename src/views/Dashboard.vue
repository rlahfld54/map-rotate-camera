<template>
  <div class="py-4 container-fluid">
    <div class="row">
      <div class="col">
        <div id="mapLayer">
          <!-- 완성된 코드 -->
            <div id="point" v-for="(item,index) in List" :key="index" 
            @click="modifyData(item)"
            :style="{top: item.x + 'px', left: item.y + 'px'}">
              <img id="look-point" src="@/assets/Polygon 1.png" width="50" height="70" alt="화각"
              :style="{ transform: 'translate(-50%,-50%)'+`rotate(${item.angle}deg)` }"
                style="top: -35px; left: 5px;">
            </div>

          <!-- 배경 이미지 -->
          <img @click="getCoordinate" class="mapimg" src="@/assets/7403915272e_l.jpg" width="600" alt="한반도">
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

          <h5>4. input창에 각도 같은 것 배열에 담아서 실제로 쓰는 것처럼 테스트 가능하게 만들기 </h5>

        </div>

        <div class="card mt-3">
          <label for="각도" style="font-size: 20px;">각도 입력</label>
          <input type="text" v-model.number="angle" />
          <button @click="getAngle">각도 입력</button>
          <br/>
          <br/>
          <div>
            <h5>1. 맨처음에는 데이터가 이미 뿌려져 있다.</h5>
            <h5>2. 이미 있는 데이터의 값을 수정해준다. ==> 빨간 점을 클릭하면 수정하는 함수가 실행된다.</h5>
            <h5>3. 새로운 데이터 값을 추가해준다. ==> input을 통해 제어한다.</h5>
          </div>
          <br/>
          <br/>
          <div>
            <p>
              두가지 경우의 기능을 만들어야한다.
            </p>
            <ul>
              <li>기존에 있는 값을 수정할때  ==> 완료</li>
              <li>새로운 값을 추가해줄때</li>
            </ul>
          </div>
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
      angle: 0,
      List: [
        { x: 338, y: 278 ,angle: 0},
        { x: 272, y: 396 ,angle: 90},
        { x: 475, y: 454 ,angle: 180},
        { x: 113, y: 82 ,angle: 90},
        { x: 60, y: 434 ,angle: 180},
        { x: 91, y: 536 ,angle: 70},
        { x: 231, y: 346 ,angle: 180},
        { x: 412, y: 184 ,angle: 200},
        { x: 540, y: 103 ,angle: 0}
      ],
      infoList: [
        {
          x: 5,
          y: 40,
          newAngle: 90
        },
        {
          x: 100,
          y: 100,
          newAngle: 180
        }
      ]
    };
  },
  mounted() {
  },
  watch: {
    // angle() {
    //   console.log(typeof this.angle)
    //   console.log(this.angle)
    // }
  },
  methods: {
    modifyData(item){
      // 해당하는 정보의 값이 객체 형태로 나온다. 수정하고 싶은 값을 바꾼다.
      console.log(item);

      // getAngle 함수에서 수정된 값을 가져온다. => 적용한다.
      item.x= 0;
      item.y= 10;
    },
    getAngle() {
      // 앵글을 바꿔주는 곳
      console.log("getAngle");
      const lookPoint = document.getElementById('look-point');
      lookPoint.style.transform = `translate( -50%, -50%) rotate( ${this.angle}deg)`;
      lookPoint.style.top = this.infoList[0].x.toString() + 'px';
      lookPoint.style.left = this.infoList[0].y.toString() + 'px';
      console.log(this.angle);
    },
    getCoordinate(e) {
      // getCoordinate ==> 새로운 값을 추가 해줄때 필요한 함수
      // 좌표 얻기 getCoordinate
      console.log(e.offsetX, e.offsetY);
      let earth = {
        x: 0, // top
        y: 0, // left
      };

      earth.x = e.offsetX;
      earth.y = e.offsetY;

      // this.List = []; // 비워준다. 두개 이상 값이 못 들어가도록..
      // this.List.push(earth);
      // console.log(this.List);

      // point의 좌표 css를 직접 바꿔준다.
      const point = document.getElementById('point');
      point.style.top = e.offsetY.toString() + 'px';
      point.style.left = e.offsetX.toString() + 'px';
      console.log(point.style.top, point.style.left);
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

/* 동그란 원 */
#point {
  position: absolute;
  width: 10px;
  height: 10px;
  background: red;
  border-radius: 50%;
  transform-origin: center;
  transform: translate(-50%, -50%);
  z-index: 9999;
}

/* 화각 이미지 */
#look-point {
  position: absolute;
  /* top: 5px;
  left: 5px; */
  /* top: -35px;
  left: 5px; */
  transform-origin: 25px 70px;
  /* transform: rotate(90deg); */
  z-index: 9999;
}
</style>
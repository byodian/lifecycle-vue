<script>
import AComponent from "./components/AComponent.vue";
import BComponent from "./components/BComponent.vue";

export default {
  name: "App",
  components: {
    AComponent,
    BComponent,
  },
  data() {
    return {
      adata: {},
      options: {},
      isShow: false,
      visibleFlag: false,
    };
  },
  watch: {
    adata: {
      handler(newData) {
        if (Object.keys(newData).length > 0) {
          this.isShow = true;
        }
        this.options = {
          xAxis: {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
          yAxis: {
            type: "value",
          },
          series: [
            {
              name: 'a',
              data: [150, 230, 224, 218, 135, 147, 260],
              type: "line",
            },
          ],
        };
      },
      deep: true,
      immediate: true,
    },
  },
  created() {
    console.log("%cparent created", "color: pink");
    const promise = new Promise((resolve) => {
      setTimeout(() => {
        resolve("123");
      }, 0);
    });

    promise.then((data) => {
      this.adata = {
        name: `byodian${data}`,
        age: "21",
        items: [1, 2, 4],
      };
    });
  },
  mounted() {
    console.log("parent mounted");
  },
  beforeUpdate() {
    console.log("parent beforeUpdate");
  },
  updated() {
    console.log("parent updated");
  },
};
</script>

<template>
  <div id="app">
    <AComponent :adata="adata" v-if="isShow"/>
    <div class="b-com-wrapper" v-if="isShow">
      <BComponent
        :options="options"
        width="100%"
        height="100%"
      />
    </div>
  </div>
</template>

<style>
p {
  margin: 0;
}

#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  height: 300px;

  outline: 1px dashed #000;
}

.b-com-wrapper {
  width: 100%;
  flex-basis: 100%;
  outline: 1px dashed pink;
}
</style>

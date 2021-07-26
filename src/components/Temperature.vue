<template>
  <div
    class="w-screen h-screen flex 	justify-center items-center"
    :class="{ 'bg-blue-200': color === 'cold', 'bg-pink-200': color === 'hot' ,'bg-yellow-200': color === 'normal' }"
  >
    <div>
      <div class="w-80 md:w-32 lg:w-96 bg-white h-80 rounded-lg	 flex flex-col justify-center items-center shadow-xl ">
        <div class="mb-4 font-bold text-2xl text-gray-600	"> {{name}} </div>
        <div class="space-x-3 bg-gray-200 w-40 cursor-pointer rounded-full shadow-inner font-bold text-gray-400">
          <button
            class="transition delay-100 duration-250 ease-in-out w-10 h-10 my-2 rounded-full "
            :class="{'bg-white shadow-xl font-bold text-yellow-500': unit === 'celsius'}"
            @click="setVisibilityUnit('celsius')"
          >
            °C
          </button>
          <button
            class="transition delay-100 duration-250 ease-in-out w-10 h-10 my-2 rounded-full "
            :class="{'bg-white shadow-xl font-bold text-blue-500': unit === 'fahrenheit'}"
            @click="setVisibilityUnit('fahrenheit')"
          >
            °F
          </button>
          <button 
            class="w-10 h-10 my-2 rounded-full"
            :class="{'bg-white shadow-xl font-bold text-green-500': unit === 'kelvin'}"
            @click="setVisibilityUnit('kelvin')"
          > K
          </button>
        </div>
        <div class="text-xl mt-8">{{showUnitName}}</div>
        <div class="text-4xl font-black">
          <div v-show=" unit === 'celsius'" class="w-32 relative">
            <input v-model="celsius" type="number" class="focus:outline-none text-center w-32">
            <div class="absolute top-0 right-2">°</div>
          </div>
          <div v-show=" unit === 'fahrenheit'" class="w-32 relative">
            <input v-model="fahrenheit" type="number" class="focus:outline-none text-center w-32">
            <div class="absolute top-0 right-2">°</div>
          </div>
          <div v-show=" unit === 'kelvin'"><input v-model="kelvin" type="number" class="focus:outline-none text-center  w-32"></div>
        </div>
      </div>
      <div class="w-80 md:w-32 lg:w-96 bg-white h-16 rounded-lg	 flex justify-center items-center shadow-xl mt-2 space-x-5">
        <a class=" text-gray-400 hover:font-bold hover:text-gray-800" href="https://github.com/indexhui/vue-temperature-converter" target="_blank">Github</a>
        <a class=" text-gray-400 hover:font-bold hover:text-gray-800" href="https://indexhui.github.io/react-temperature-converter/" target="_blank">React</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // name: 'HelloWorld',
  data () {
    return {
      unit: "celsius",
      color: "cold",
      celsius: 0,
      fahrenheit: 32,
      kelvin: 273.15,
    }
  },
  methods: {
    setVisibilityUnit(unit) {
      this.unit = unit;
    },
    cToFahr(){
      return this.celsius * 9 / 5 + 32
    },
    cToKel(){
      return (this.celsius*100 + 27315)/100
    },
    fToCel(){
      return Math.round((this.fahrenheit - 32)* 5 / 9 * 100) /100
    },
    fToKel(){
      return Math.round((this.fahrenheit*100 + 45967)* 5 / 9)/100
    },
    kToCel(){
      return Math.round(this.kelvin*100 - 27315)/100
    },
    kToFahr(){
      return Math.round((this.kelvin*9/5)*100-45967)/100
    }
  },
  watch: {
    celsius: {
      handler: function(){
        if (this.unit === 'celsius') {
          this.fahrenheit = this.cToFahr()
          this.kelvin = this.cToKel()
        }
        if (this.celsius > 28) {
          this.color = "hot"
        } else if (this.celsius  < 20) {
          this.color ='cold'
        } else {
          this.color ='normal'
        }
      },
    },
    fahrenheit: {
      handler: function(){
        if (this.unit === 'fahrenheit') {
          this.celsius = this.fToCel()
          this.kelvin = this.fToKel()
        }
      },
    },
    kelvin: {
      handler: function(){
        if (this.unit === 'kelvin') {
          this.celsius = this.kToCel()
          this.fahrenheit = this.kToFahr()
        }
      },
    },
  },
  computed: {
    showUnitName(){
      return this.unit.charAt(0).toUpperCase() + this.unit.slice(1)
    }
  },
  props: {
    name: String
  }
}
</script>

<style scoped>
input[type='number']::-webkit-inner-spin-button, 
input[type='number']::-webkit-outer-spin-button { 
    -webkit-appearance: none;
    margin: 0;
  }

  input {
    white-space:nowrap;
  }
  
</style>

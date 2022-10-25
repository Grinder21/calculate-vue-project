<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div
    class="p-3 rounded"
    style="max-width: 400px; margin: 50px auto; background: #6332a8"
  >
    <!-- total result -->
    <div
      class="w-full rounded m-1 p-3 text-end lead font-weight-bold text-white bg-vue-dark"
    >
      {{ calculatorValue || 0 }}
    </div>
    <!-- buttons for calculate -->
    <div class="row no-gutters">
      <div class="col-3" v-for="element in calculatorElements" :key="element">
        <div
          class="lead text-white text-center m-1 py-2 bg-vue-dark rounded hover-class"
          :class="{
            'bg-vue-operators': [
              'C',
              '√',
              '%',
              '/',
              '*',
              '-',
              '+',
              '=',
            ].includes(element),
          }"
          @click="action(element)"
        >
          {{ element }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Calculate',
  props: {
    msg: String,
  },
  data() {
    return {
      calculatorValue: '',
      calculatorElements: [
        'C',
        '√',
        '%',
        '/',
        7,
        8,
        9,
        '*',
        4,
        5,
        6,
        '-',
        1,
        2,
        3,
        '+',
        '00',
        0,
        ',',
        '=',
      ],
      operator: null,
      previousCalculatorValue: '',
    }
  },
  methods: {
    action(element) {
      /* append value */
      if (!isNaN(element) || element === ',') {
        this.calculatorValue += element + ''
      }

      /* clear value */
      if (element === 'C') {
        this.calculatorValue = ''
      }

      /* get percentage at enter value */
      if (element === '%') {
        this.calculatorValue = this.calculatorValue / 100 + ''
      }

      if (element === '√') {
        this.calculatorValue = Math.sqrt(this.calculatorValue) + ''
      }

      if (['/', '*', '-', '+'].includes(element)) {
        this.operator = element
        this.previousCalculatorValue = this.calculatorValue
        this.calculatorValue = ''
      }

      if (element === '=') {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        )

        this.previousCalculatorValue = ''
        this.operator = null
      }
    },
  },
}
</script>

<style scoped>
.bg-vue-dark {
  background: #a509ff;
}
.hover-class:hover {
  cursor: pointer;
  background: #6f03fc;
}
.bg-vue-operators {
  background: #8b32a8;
}
</style>

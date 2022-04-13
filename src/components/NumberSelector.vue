<template>
  <div>
    <div
      class="number"
      :id="'number-'+number"
      v-for="number in n()"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  //When using the data property, the value must be a function that returns an object
  data: function() {
    return {
      //Added a multiword name for component as this prevents conflict with existing and future html elements since all HTML elements are a single word.
      name: 'NumberSelector',
      limit: this.$parent.limit,
      numbers: []
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    n()
    {
      // 0 has no divisors and therefore I have made that the lowest number in the array is 1
      for(var i = 1; i < this.limit; i++)
      if (this.limit.length == 0){
        return 1;
      }
      /* instead of using a for loop, I have used a spread array which maps through the array of numbers and converts
      the string of numbers into an integer.
      This improves overall amount of code, code readability and overall performance when reloading the array
      */
      let numbersArray = [...Array(parseInt(this.limit))].map((_, i) => i + 1);
      return numbersArray.sort(() => Math.random() - 0.5);
    },
    hov(number)
    {
      const nums = document.querySelectorAll('.number');
      for(let i = 0; i < nums.length; i++)
      {
        const num = nums[i].textContent.trim();
        if(number % num === 0)
        {
          nums[i].classList.add('active')
          //removed unnecessary console.log which printed the divisors of the hovered number
        }
      }
    },
    reset()
    {
      const nums = document.querySelectorAll('.number');
      nums.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>
//Created a seperate style file in order to improve the overall management of the component.
/* As the codebase grows, each component will be placed in their own respective folders within
the components folder so that components are easily manageable and modular. This will improve the
overall maintenance of each component and allow for easier debugging. However, it is not incorrect 
to place all the styles, javascript and html all in 1 file; I just believe that it is easier to
maintain and debug when they are seperated.
*/
<style src="./NumberSelector.css"></style>
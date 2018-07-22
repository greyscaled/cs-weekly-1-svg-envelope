<template>
  <svg
    class="svg-paper"
    id="paper"
    preserveAspectRatio="xMidYMid meet"
    height="200"
    width="200"
    viewbox="0 0 200 200"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:svg="http://www.w3.org/2000/svg">
    <g class="svg-paper__group">
      <!-- bg paper -->
      <rect
        class="svg-paper__sheet"
        id="sheet"
        fill="#FFF"
        height="100%"
        width="100%"
        x="0"
        y="0"/>
      <!-- lines -->
      <g class="svg-paper__lines">
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="20%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="30%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="40%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="50%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="60%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="70%"/>
        <rect
          class="svg-paper__line"
          fill="#BBDEFB"
          height="1%"
          width="90%"
          x="5%"
          y="80%"/>
      </g>
    </g>
  </svg>
</template>

<script>
export default {
  name: 'paper'
}
</script>

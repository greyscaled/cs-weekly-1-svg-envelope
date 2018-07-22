<template>
  <div id="svg-wrapper">
    <svg
      class="svg-envelope"
      id="envelope"
      preserveAspectRatio="xMidYMid meet"
      height="400"
      width="400"
      viewbox="0 0 400 400"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:svg="http://www.w3.org/2000/svg">
      <g class="svg-envelope__group">
        <!-- bg -->
        <rect
          class="svg-envelope__bg"
          fill="rgba(255, 202, 40, .5)"
          height="100%"
          width="100%"
          rx="20"
          ry="20"
          x="0"
          y="0"/>
        <!-- triangle/envelope -->
        <path
          :class="{
            openLid: open,
            closeLid: isClosing
          }"
          id="triangle"
          d="M20 0 L 200 200 L 380 0 L 20 0"
          fill="rgba(255, 202, 40, .5)"
          stroke="transparent"/>
        <!-- undearneath envelop -->
        <path
          d="M20 0 L 200 200 L 380 0 L 20 0"
          fill="rgba(255, 202, 40, .2)"/>
        <!-- Seal -->
        <circle
          :class="{
            openSeal: open,
            closeSeal: isClosing
          }"
          @click.stop.prevent="sealClick"
          id="seal"
          cx="200"
          cy="200"
          r="40"
          stroke="transparent"
          fill="rgba(255, 79, 79, .8)"/>
      </g>
    </svg>
    <transition name="paper-animation">
      <Paper v-if="open" />
    </transition>
  </div>
</template>

<script>
// components
import Paper from '@/components/Paper'

export default {
  name: 'envelope',
  components: { Paper },
  data () {
    return {
      isClosing: false,
      open: false
    }
  },

  methods: {
    sealClick () {
      this.open = !this.open
      // set to opposite of this.open, ensures on first click:
      // open: true, isClosing: false
      this.isClosing = !this.open
    }
  }
}
</script>

<style>
/* wrap the SVGs to overlap them */
#svg-wrapper {
  height: 200px;
  position: relative;
}

#paper {
  clip-path: polygon(50% 50%, 0 0, 100% 0);
  left: 0;
  position: absolute;
  transform: scale(.5);
  top: 0;
}

/* paper animation classes */
.paper-animation-enter-active {
  animation: popup .5s ease-in;
}

@keyframes popup {
  0% { opacity: 0 };
  50% { opacity: 0 };
  51% {
    opacity: 1;
  }
  90% {
    transform: translateZ(1px);
  }
}

.paper-animation-leave-active {
  animation: fadeout .3s ease-out;
}

@keyframes fadeout {
  0% { opacity: 1 }
  100% {
    opacity: 0;
    transform: translateZ(-1px);
  }
}

#seal {
  cursor: pointer;
}

/* lid/triangle animation classes */
.closeLid {
  animation: revRotX .5s ease-in;
}

.openLid {
  animation: rotX .5s ease-in forwards;
}

@keyframes revRotX {
  0% { transform: rotateX(180deg); }
  100% { transform: rotateX(0deg); }
}

@keyframes rotX {
  0% { transform: rotateX(0deg); }
  100% { transform: rotateX(180deg); }
}

/* seal/circle animation classes */
.closeSeal, .openSeal {
  transform-origin: 200px 200px;
}

.closeSeal {
  animation: replaceSeal .6s ease-in;
  clip-path: none;
}

.openSeal {
  animation: transX .5s ease-in forwards;
}

@keyframes replaceSeal {
  0% { transform: translateY(-395px); }
  /* prevents odd bug where 1/2 the circle doesnt show */
  100% { opacity: 1; }
}

@keyframes transX {
  0% { transform: translateY(0); }
  50% {
    /* cutout places seal "behind" lid */
    clip-path: polygon(
      50% 50%,
      0% 100%,
      0% 0%,
      100% 0%,
      100% 100%
    );
  }
  100% {
    clip-path: polygon(
      50% 50%,
      0% 100%,
      0% 0%,
      100% 0%,
      100% 100%
    );
    transform: translateY(-395px);
  }
}
</style>

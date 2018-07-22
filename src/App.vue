<template>
  <div class="container" id="app">
    <!-- Headinng -->
    <div class="row">
      <div class="col s12">
        <transition name="heading-transition" appear>
          <h1>SVG Envelope</h1>
        </transition>
      </div>
    </div>
    <!-- SVG -->
    <div class="row">
      <div class="col s12 envelope-wrapper">
        <transition name="envelope-animate" appear>
          <Envelope />
        </transition>
      </div>
    </div>
    <!-- Page Footer -->
    <transition name="footer-transition" appear>
      <Footer />
    </transition>
  </div>
</template>

<script>
// components
import Envelope from '@/components/Envelope'
import Footer from '@/components/Footer'

export default {
  name: 'app',
  components: { Envelope, Footer }
}
</script>

<style>
body {
  background-color: rgba(255, 102, 252, .38);
}

/* set default font */
#app {
  font-family: 'Permanent Marker', cursive;
}

/* Envelope svg properties */
#envelope {
  /* needed if animation goes outside svg area */
  overflow: visible;
  transform-origin: 0 0;
  transform: scale(.5);
}

.envelope-wrapper {
  height: 200px;
  margin-top: 70px;
}

.envelope-animate-enter {
  clip-path: circle(1%);
  transform: translateX(-200px);
}

.envelope-animate-enter-active {
  animation: rollIn 2s ease-in;
}

@keyframes rollIn {
  0% {
    clip-path: circle(1%);
    transform: translateX(-200px);
  }

  50% {
    clip-path: circle(1%);
  }

  100% {
    clip-path: circle(100%);
  }
}

/* easing in the heading */
.heading-transition-enter-active {
  animation: fadeIn 1s ease-in;
}

/* easing in the Footer */
.footer-transition-enter-active {
  animation: fadeIn 1s ease-in;
}

@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
</style>

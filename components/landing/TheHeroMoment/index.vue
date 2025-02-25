<template>
  <article class="the-hero-moment">
    <MetalGrid>
      <div class="the-hero-moment__container">
        <VersionInfo
          class="the-hero-moment__version-info"
          :version="version"
        />
        <h1 class="the-hero-moment__title">
          Open-Source Quantum Development
        </h1>
        <p class="the-hero-moment__description">
          Qiskit {{ qiskitPronuntiation }} is an open source SDK for working with quantum
          computers at the level of pulses, circuits and application modules.
        </p>
        <AppCta
          class="the-hero-moment__cta"
          v-bind="getStartedLink"
        />
      </div>
    </MetalGrid>
  </article>
</template>

<script lang="ts">
import Vue from 'vue'

import { Prop, Component } from 'vue-property-decorator'

@Component
export default class TheHeroMoment extends Vue {
  @Prop({ type: String, required: true }) version!: string
  getStartedLink = {
    url: 'https://qiskit.org/documentation/getting_started.html',
    label: 'Get started',
    segment: { action: 'Get started' }
  }

  data () {
    return { qiskitPronuntiation: Math.random() < 0.5 ? '[kiss-kit]' : '[quiss-kit]' }
  }
}
</script>

<style lang="scss">
@import '~carbon-components/scss/globals/scss/typography';

.the-hero-moment {
  //@include responsive-grid-bg-strip('/images/grid/grid-hero.svg', auto, 56rem);

  position: relative;
  overflow: hidden;
  //padding-top: $layout-05;
  margin-bottom: $layout-05;
  // In Figma, the height is not enforced but the background is always
  // visible completely so we do it in the CSS. A small correction is needed
  // to be able of displaying the bottom lines of the grid.
  height: calc(56rem + 2px);

  @include mq($from: medium, $until: large) {
    margin-bottom: $layout-06;
    // To adjust to the size of the smaller grid.
    height: calc(#{56rem * 40 / 64} + 2px);
  }

  @include mq($until: medium) {
    margin-bottom: 0;
    // To adjust to the size of the smaller grid.
    height: calc(#{56rem * 40 / 64} + 2px);
  }

  &__square-link {
    width: 4rem;
    height: 4rem;
    background-color: $cool-gray-100;
    position: absolute;
    top: 21%;
    left: 43%;
  }

  &__container {
    @include contained();

    position: relative;
    background-image: url("/images/landing-page/hero-illustration.png");
    background-position: right center;
    background-repeat: no-repeat;
    background-size: 70% auto;
    padding-top: $layout-05;

    pointer-events: none;

    @include mq($from: medium, $until: large) {
      background-size: contain;
    }

    @include mq($until: medium) {
      background-image: none;
    }
  }

  &__version-info {
    margin: $layout-01 0 $layout-05;

    @include mq($from: medium, $until: large) {
      margin: 0 0 $layout-03;
    }

    @include mq($until: medium) {
      // Differs from Figma to make it match with medium spacer.
      margin: 0 0 $layout-03;
    }
  }

  &__title {
    @include type-style('productive-heading-07');
    color: $white-text-01;
    margin: 0 0 $layout-05;
    max-width: 6 * $column-size-large;
    // TODO: Force pointer events to allow the user to select text. Remove
    // when decomissioning the Metal page.
    pointer-events: auto;

    @include mq($from: medium, $until: large) {
      @include type-style('productive-heading-06');
      // Notice the difference with the small version. This space is much more
      // small since it is in the spacing scale.
      margin: 0 0 $spacing-03;
      max-width: 4 * $column-size-medium;
    }

    @include mq($until: medium) {
      @include type-style('productive-heading-04');
      margin: 0 0 $layout-03;
      max-width: 4 * $column-size-medium;
    }
  }

  &__description {
    @include type-style('body-long-01');
    color: $cool-gray-80;
    max-width: 5 * $column-size-large;
    margin: 0 0 $layout-06;
    // TODO: Force pointer events to allow the user to select text. Remove
    // when decomissioning the Metal page.
    pointer-events: auto;

    @include mq($from: medium, $until: large) {
      max-width: 3 * $column-size-medium;
      margin-bottom: $layout-05;
    }

    @include mq($until: medium) {
      max-width: 3 * $column-size-small;
      margin-bottom: $layout-03;
    }
  }

  &__cta {
    // TODO: Force pointer events to allow the user to select text. Remove
    // when decomissioning the Metal page.
    pointer-events: auto;
  }
}
</style>

<template>
  <header class="app-page-header">
    <div class="app-page-header__container">
      <main class="app-page-header__main">
        <div>
          <h1 class="app-page-header__headline copy__page-title">
            <slot name="title" />
          </h1>
          <div class="app-page-header__description">
            <p
              v-for="(paragraph, index) in description"
              :key="index"
              class="copy__paragraph"
              v-text="paragraph"
            />
          </div>
        </div>
        <AppCta v-if="cta" v-bind="cta" />
      </main>
      <aside class="app-page-header__aside">
        <div>
          <div class="app-page-header__card-title-wrapper">
            <div class="app-page-header__card-title copy__subtitle" v-text="cardTitle" />
          </div>
          <slot name="card" />
        </div>
      </aside>
    </div>
  </header>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component, Prop } from 'vue-property-decorator'
import { GeneralLink } from '~/constants/appLinks'

@Component
export default class AppPageHeaderWithCard extends Vue {
  @Prop({ type: String, required: true }) cardTitle!: string
  @Prop({ type: Object, required: true }) cta!: GeneralLink
  @Prop({ type: Array, required: true }) description!: string[]
}
</script>

<style lang="scss" scoped>
@import "~/assets/scss/blocks/copy.scss";

.app-page-header {
  @include responsive-grid-bg-strip("/images/grid/grid-hero-learn.svg", auto, 28rem);
  padding-top: $layout-06;

  @include mq($until: medium) {
    padding-top: $layout-04;
  }

  &__container {
    @include contained();
    display: grid;
    column-gap: $spacing-07;
    grid-template-columns: 1fr auto;

    @include mq($until: large) {
      grid-template-columns: 1fr 1fr;
    }

    @include mq($until: medium) {
      grid-template-columns: 1fr;
    }
  }

  &__main {
    display: flex;
    flex-flow: column;
    gap: $spacing-05;
    justify-content: space-between;

    @include mq($until: x-large) {
      gap: $spacing-06;
    }

    @include mq($until: large) {
      gap: $spacing-09;
    }
  }

  &__headline {
    margin-top: $spacing-07;
  }

  &__description {
    margin-top: $spacing-05;

    @include mq($until: x-large) {
      margin-top: $spacing-06;
    }

    @include mq($until: large) {
      margin-top: $spacing-09;
    }
  }

  &__aside {
    max-width: 18rem;
    width: 100%;

    @include mq($until: large) {
      max-width: initial;
    }

    @include mq($until: medium) {
      margin-top: $spacing-09;
    }
  }

  &__card-title {
    border-bottom: 4px solid $purple-60;
    display: inline;
    padding-bottom: $spacing-02;
    padding-right: $spacing-03;

    &-wrapper {
      margin-bottom: $spacing-06;
    }
  }
}
</style>

<template>
  <div class="supporting-image">
    <!-- <style>{{ style }}</style> -->
    <component
      v-for="(key, i) in SectionKeys"
      :key="key"
      :is="Sections.get(key).image"
      class="layer"
      :visible="i <= sectionIndex"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { Sections, SectionKeys } from '../constants.js';

const sectionKey = ref(String);
const sectionIndex = computed(() => SectionKeys.indexOf(sectionKey.value));

const style = computed(() => {
  const background = Sections.get(sectionKey.value).color;
  return `
    .supporting-image {
      background-color: ${background};
    }
    .layer .fill-bg {
      fill: ${background};
    }
  `;
});
</script>

<style scoped lang="scss">
.supporting-image {
  overflow: hidden;
  perspective: 1000px;
  position: relative;
  text-align: center;
  transition: background-color 0.5s;

  @media print {
    display: none;
  }
}

.layer {
  left: 50%;
  margin-left: -50%;
  margin-top: -110%;
  position: absolute;
  top: 70%;
  width: 100%;

  @media screen and (min-width: 1000px) {
    margin-left: -250px;
    margin-top: -550px;
    width: 500px;
  }
}
</style>

<style lang="scss">
.layer {
  .stroke {
    fill: none;
    stroke: #fff;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-width: 2px;
  }

  .fill {
    fill: #fff;
  }

  .fill-bg {
    transition: fill 0.5s;
  }
}
</style>






<!-- <script>
import { Sections, SectionKeys } from '../constants.js';

export default {
  name: 'SupportingImage',
  props: {
    sectionKey: String,
  },
  computed: {
    style() {
      const background = Sections.get(this.sectionKey).color;
      return `
          .supporting-image {
            background-color: ${background};
          }
          .layer .fill-bg {
            fill: ${background};
          }
        `;
    },
  },
  render() {
    const { style } = this;
    const sectionIndex = SectionKeys.indexOf(this.sectionKey);

    return (
      <div class="supporting-image">
        <style>{style}</style>
        {SectionKeys.map((key, i) => {
          const Layer = Sections.get(key).image;
          return <Layer class="layer" visible={i <= sectionIndex} />;
        })}
      </div>
    );
  },
};
</script>

<style scoped lang="scss">
.supporting-image {
  // Background defined in component
  overflow: hidden;
  perspective: 1000px;
  position: relative;
  text-align: center;
  transition: background-color 0.5s;

  @media print {
    display: none;
  }
}

.layer {
  left: 50%;
  margin-left: -50%;
  margin-top: -110%;
  position: absolute;
  top: 70%;
  width: 100%;

  @media screen and (min-width: 1000px) {
    margin-left: -250px;
    margin-top: -550px;
    width: 500px;
  }
}
</style>

<style lang="scss">
.layer {
  .stroke {
    fill: none;
    stroke: #fff;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-width: 2px;
  }

  .fill {
    fill: #fff;
  }

  .fill-bg {
    // Fill defined in component
    transition: fill 0.5s;
  }
}
</style> -->

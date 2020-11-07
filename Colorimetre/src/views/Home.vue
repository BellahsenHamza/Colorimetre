<template>
  <div class="home">
    <h1>Colorimetre</h1>
    <!--instances de colorimetre -->
    <selection-couleur
      v-for="color in specs"
      :couleur-hex="color.code"
      :nom-couleur="color.label"
      v-bind:key="color.code"
      @value-changed="(val) => updateValue('red', val)"
    />

    <!--couleur finale -->
    <div class="finale" :style="{ backgroundColor: blend }" />
  </div>
</template>

<script>
import SelectionCouleur from '@/components/SelectionCouleur.vue';

export default {
  name: 'Home',
  components: {
    SelectionCouleur,
  },
  data() {
    return {
      specs: [
        { label: 'Rouge', code: 'red' },
        { label: 'Bleu', code: 'blue' },
        { label: 'Vert', code: 'green' },
      ],
      values: {
        red: 0,
        green: 0,
        blue: 0,
      },
    };
  },
  methods: {
    updateValue(key, value) {
      this.values[key] = value;
    },
  },
  computed: {
    blend() {
      return `rgb(${this.values.red},${this.values.green},${this.values.blue})`;
    },
  },
};
</script>

<style>
.finale {
  width: 60px;
  height: 60px;
  display: inline-block;
}
</style>

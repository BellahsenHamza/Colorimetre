<template>
  <div class="selection-couleur">
    <div class="square" :style="{ backgroundColor: couleurHex }" />
    <div class="label">
      {{ nomCouleur }}
    </div>
    <div>
      <input
        type="range"
        min="0"
        max="255"
        v-model.number="valeurCourante"
        @input="changed"
      />
    </div>
    <div>{{ valeurPourcentage }} %</div>
  </div>
</template>

<script>
export default {
  name: 'selection-couleur',
  props: {
    nomCouleur: {
      type: String,
      required: true,
    },
    couleurHex: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      valeurCourante: 0,
    };
  },
  computed: {
    valeurPourcentage() {
      return Math.round((this.valeurCourante / 255) * 100);
    },
  },
  methods: {
    changed() {
      this.$emit('value-changed', this.valeurCourante);
    },
  },
};
</script>

<style lang="scss" scoped>
.selection-couleur {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 1em;
  .label {
    width: 200px;
  }
  > div {
    padding-right: 0.5em;
    padding-left: 0.5em;
  }
  .square {
    height: 30px;
    width: 30px;
  }
}
</style>

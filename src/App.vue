<template>
  <div class="h-screen text-slate-200" :class="backgroundColor">
    <Configuration
      @update:keySuccess="updateKeySuccess"
      @update:keyFailure="updateKeyFailure"
      @update:minSuccess="updateMinSuccess"
      @update:maxSuccess="updateMaxSuccess"
    />
    <Output
      :minSuccess="minSuccess"
      :maxSuccess="maxSuccess"
      :keySuccess="keySuccess"
      :keyFailure="keyFailure"
      @update:win="updateWin"
    />
  </div>
</template>

<script lang="ts">
import Configuration from './components/Configuration.vue';
import Output from './components/Output.vue';

export default {
  components: {
    Configuration,
    Output,
  },
  data() {
    return {
      keySuccess: '1',
      keyFailure: '2',
      minSuccess: 8,
      maxSuccess: 10,
      win: false,
      backgroundColor: 'bg-slate-800',
    };
  },
  methods: {
    updateKeySuccess(key: string) {
      this.keySuccess = key;
    },
    updateKeyFailure(key: string) {
      this.keyFailure = key;
    },
    updateMinSuccess(newMinSuccess: number) {
      this.minSuccess = newMinSuccess;
    },
    updateMaxSuccess(newMaxSuccess: number) {
      this.maxSuccess = newMaxSuccess;
    },
    updateWin(win: boolean) {
      this.win = win;
      this.backgroundColor = win ? 'bg-green-800' : 'bg-red-800';
    },
  },
};
</script>

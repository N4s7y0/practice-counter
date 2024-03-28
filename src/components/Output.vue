<template>
  <div
    class="flex flex-row items-center gap-16 min-h-56"
    :class="backGroundColor"
    @keydown="handleKeyDown"
    tabindex="0"
  >
    <div class="flex flex-col">
      <p v-for="(item, index) in items" :key="index">{{ item }}</p>
    </div>
    <p>{{ successes }} / {{ successes + failures }}</p>
    <p v-if="win">Congrats! You passed with {{ lastWin }}</p>
    <p v-if="loss">Unfortunately you suck! You lost with {{ lastLoss }}</p>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      items: [],
      successes: 0,
      failures: 0,
      win: false,
      loss: false,
      lastWin: '',
      lastLoss: '',
      backGroundColor: 'bg-slate-700',
    };
  },
  props: {
    keySuccess: String,
    keyFailure: String,
    minSuccess: Number,
    maxSuccess: Number,
  },
  methods: {
    handleKeyDown(event) {
      if (event.key === this.keySuccess) {
        this.items.push('Yay');
        this.successes++;
        this.backGroundColor = 'bg-green-800';
      }
      if (event.key === this.keyFailure) {
        this.items.push('Noes');
        this.failures++;
        this.backGroundColor = 'bg-red-800';
      }
      if (this.successes + this.failures >= this.maxSuccess) {
        if (this.successes >= this.minSuccess) {
          this.win = true;
          this.loss = false;
          this.lastWin = this.successes + ' / ' + (this.successes + this.failures);
        } else {
          this.loss = true;
          this.win = false;
          this.lastLoss = this.successes + ' / ' + (this.successes + this.failures);
        }
        this.$emit('update:win', this.win);
        this.reset();
      }
    },
    reset() {
      this.items = [];
      this.successes = 0;
      this.failures = 0;
    },
  },
};
</script>

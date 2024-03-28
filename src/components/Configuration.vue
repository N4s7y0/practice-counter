<template>
  <div class="flex flex-col">
    <div class="px-16 py-8 mx-auto bg-gray-900 w-800">
      <h1 class="text-xl">Configuration</h1>
      <p>Input for Success</p>
      <button
        class="px-4 py-2 font-bold text-white bg-green-900 rounded hover:bg-green-700"
        border-red-500:editSuccess
        @click="editSuccess = !editSuccess"
        @keydown="handleKeyDownSuccess"
      >
        {{ keySuccess }}
      </button>
      <p>Input for Failure</p>
      <button
        class="px-4 py-2 font-bold text-white bg-red-900 rounded hover:bg-red-700"
        border-red-500:editFailure
        @click="editFailure = !editFailure"
        @keydown="handleKeyDownFailure"
      >
        {{ keyFailure }}
      </button>
      <p>Needed Success Rate</p>
      <input type="number" class="w-8 text-gray-900 bg-gray-200" v-model="minSuccess" /> /
      <input type="number" class="w-8 text-gray-900 bg-gray-200" v-model="maxSuccess" />
      <!-- todo: make a proper layout -->
      <br />
      <!-- todo: focus the div in output when this button is pressed -->
      <button
        class="px-4 py-2 font-bold text-white rounded bg-slate-700 hover:bg-slate-500"
      >
        Start
      </button>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      editSuccess: false,
      keySuccess: '1',
      editFailure: false,
      keyFailure: '2',
      minSuccess: 8,
      maxSuccess: 10,
    };
  },
  methods: {
    handleKeyDownSuccess(event: any): void {
      if (this.editSuccess) {
        this.keySuccess = event.key;
        this.$emit('update:keySuccess', this.keySuccess);
      }
    },
    handleKeyDownFailure(event: any): void {
      if (this.editFailure) {
        this.keyFailure = event.key;
        this.$emit('update:keyFailure', this.keyFailure);
      }
    },
  },
  watch: {
    minSuccess(newMinSuccess) {
      this.$emit('update:minSuccess', newMinSuccess);
    },
    maxSuccess(newMaxSuccess) {
      this.$emit('update:maxSuccess', newMaxSuccess);
    },
  },
};
</script>

<template>
  <form class="create-twiit-panel" @submit.prevent="createNewTwiit" :class="{ '--exceeded': newTwiitCharacterCount > 180 }">
    <label for="newTwiit"><strong>New Twiit</strong> ({{ newTwiitCharacterCount }}/180)</label>
    <textarea id="newTwiit" rows="4" v-model="state.newTwiitContent"/>

    <div class="create-twiit-panel__submit">
      <div class="create-twiit-type">
        <label for="newTwiitType"><strong>Type: </strong></label>
        <select id="newTwiitType" v-model="state.selectedTwiitType">
          <option :value="option.value" v-for="(option, index) in state.twiitTypes" :key="index">
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>
        Twiit It!
      </button>
    </div>
  </form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  name: "CreateTwiitPanel",
  setup(props, ctx) {
    const state = reactive({
      newTwiitContent: '',
      selectedTwiitType: 'instant',
      twiitTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Twiit'}
      ]
    })

    const newTwiitCharacterCount = computed(() => state.newTwiitContent.length)

    function createNewTwiit() {
      if (state.newTwiitContent && state.selectedTwiitType !== 'draft') {
        ctx.emit('add-twiit', state.newTwiitContent);
        state.newTwiitContent = '';
      }
    }

    return {
      state,
      newTwiitCharacterCount,
      createNewTwiit
    }
  }
};
</script>

<style lang="scss" scoped>
.create-twiit-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;

  textarea {
    border: 1px solid #DFE3E8;
    border-radius: 5px;
  }

  .create-twiit-panel__submit {
    display: flex;
    justify-content: space-between;

    .create-twiit-type {
      padding: 10px 0;
    }

    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
    }
  }

  &.--exceeded {
    color: red;
    border-color: red;

    .create-twiit-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>
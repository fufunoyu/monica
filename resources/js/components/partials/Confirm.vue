<template>
  <div>
    <p>
      <a :class="lclass" :title="title" href="" @click.prevent="open">
        <slot>
        </slot>
      </a>
    </p>

    <sweet-modal ref="modal" tabindex="-1" role="dialog">
      <div>
        {{ message }}
      </div>

      <!-- Modal Actions -->
      <div slot="button" class="flex-ns justify-between">
        <a class="btn mt2" href="" @click.prevent="close">
          {{ $t('app.cancel') }}
        </a>
        <button class="btn btn-primary w-auto-ns w100 mt2 pb0-ns" @click="confirm($event)">
          {{ $t('app.confirm') }}
        </button>
      </div>
    </sweet-modal>
  </div>
</template>

<script>
import { SweetModal } from 'sweet-modal-vue';

export default {

  components: {
    SweetModal,
  },

  props: {
    title: {
      type: String,
      default: '',
    },
    message: {
      type: String,
      default: '',
    },
    linkClass: {
      type: [String, Array],
      default: '',
    },
  },

  computed: {
    lclass() {
      return this.linkClass == '' ? 'pointer' : this.linkClass;
    }
  },

  methods: {
    open() {
      this.$refs.modal.open();
    },
    close() {
      this.$refs.modal.close();
    },
    confirm(event) {
      this.close();
      this.$emit('confirm', event);
    }
  }

};
</script>

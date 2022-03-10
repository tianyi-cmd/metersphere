<template>
  <api-base-component
    @copy="copyRow"
    @remove="remove"
    @active="active"
    :data="beanShellProcessor"
    :draggable="draggable"
    :color="color"
    :is-max="isMax"
    :show-btn="showBtn"
    :background-color="backgroundColor"
    :title="title" v-loading="loading">

    <legend style="width: 100%">
      <beanShell-processor-content
        :beanShell-processor="beanShellProcessor"
        :is-pre-processor="isPreProcessor"
        :node="node"
        :is-read-only="true"/>
    </legend>

  </api-base-component>
</template>

<script>
import MsCodeEdit from "../../../../common/components/MsCodeEdit";
import MsInstructionsIcon from "../../../../common/components/MsInstructionsIcon";
import MsDropdown from "../../../../common/components/MsDropdown";
import ApiBaseComponent from "../common/ApiBaseComponent";
import BeanShellProcessorContent from "../common/BeanShellProcessorContent";

export default {
  name: "MsBeanShellProcessor",
  components: {BeanShellProcessorContent, ApiBaseComponent, MsDropdown, MsInstructionsIcon, MsCodeEdit},
  props: {
    draggable: {
      type: Boolean,
      default: false,
    },
    isMax: {
      type: Boolean,
      default: false,
    },
    showBtn: {
      type: Boolean,
      default: true,
    },
    isReadOnly: {
      type: Boolean,
      default:
          false
      },
    beanShellProcessor: {
        type: Object,
      },
    isPreProcessor: {
      type: Boolean,
      default:
        false
    },
    title: String,
    color: String,
    backgroundColor: String,
    node: {},
  },
  data() {
    return {loading: false}
  },
  methods: {
    remove() {
      this.$emit('remove', this.beanShellProcessor, this.node);
    },
    copyRow() {
      this.$emit('copyRow', this.beanShellProcessor, this.node);
    },
    reload() {
      this.loading = true
      this.$nextTick(() => {
        this.loading = false
      })
    },
    active() {
      this.beanShellProcessor.active = !this.beanShellProcessor.active;
      this.reload();
    },
  }
  }
</script>

<style scoped>
  /deep/ .el-divider {
    margin-bottom: 10px;
  }
</style>

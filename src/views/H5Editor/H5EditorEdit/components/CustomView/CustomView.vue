<template>
  <div class="h5custom" v-if="editItem">
    <div class="h5custom-btn"
         :style="{
            width: editItem.w + 'px',
            height: editItem.h + 'px',
            lineHeight: editItem.h + 'px',
            color: editItem.style.color,
            background: editItem.style.background,
            borderRadius: editItem.style.borderRadius + 'px',
            opacity: editItem.style.opacity,
            fontSize: editItem.style.fontSize + 'px'
         }">
         {{ editItem.label }}
    </div>
  </div>
</template>

<script>
export default {
    name: 'CustomView',
    props: {
        editItem: Object
    },
}
</script>

<style lang="scss" scoped>
.h5custom{
  &-btn{
    text-align: center;
  }
}
</style>

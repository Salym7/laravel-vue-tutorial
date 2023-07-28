<template>
  <td
    class="table__body-cell"
    :class="{
      'table__body-cell_actions': type === 'actions',
    }"
  >
    <div class="user-avatar user-avatar_size_s" v-if="type === 'avatar'">
      <div class="user-avatar__wrapper">
        <img :src="src" alt="avatar" class="user-avatar__image" />
      </div>
    </div>
    <a :href="href" v-else-if="type === 'link'"
      ><slot>{{ value }}</slot></a
    >
    <slot v-else>{{ value }}</slot>
  </td>
</template>

<script setup lang="ts">
import { BodyColumnType } from "@/shared/ui/TableBodyRow.types"

const value = "Отредактируй меня"

defineProps<{
  type?: BodyColumnType
  title?: string
  minWidth?: boolean
  href?: string
  src?: string
}>()
</script>

<style scoped></style>

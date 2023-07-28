<template>
  <th
    class="table__head-cell"
    :class="{
      'table__head-cell_actions': type === 'actions',
      'table__head-cell_width_min': minWidth,
    }"
  >
    <template v-if="type === 'actions'">
      <a
        class="button button_no-text button_size_xs button_transparent"
        href="#"
      >
        <svg class="icon icon_type_cog">
          <use xlink:href="@/shared/assets/i/sprite/sprite.svg#cog"></use>
        </svg>
      </a>
      <a
        class="button button_no-text button_size_xs button_transparent"
        href="#"
      >
        <svg class="icon icon_type_filter">
          <use xlink:href="@/shared/assets/i/sprite/sprite.svg#filter"></use>
        </svg>
      </a>
    </template>

    <div class="table__head-cell-inner" v-else-if="title" @click="handleClick">
      <span>{{ title }}</span>
      <Icon type="arrow-up" v-if="sortDir === 'desc'" />
      <Icon type="arrow-down" v-else-if="sortDir === 'asc'" />
    </div>
  </th>
</template>

<script setup lang="ts">
import { ColumnType } from "@/shared/ui/TableHeadRow.types"
import Icon from "@/shared/ui/Icon.vue"
import { TAvailableSorting } from "./Table.type"

const props = defineProps<{
  type?: ColumnType
  title?: string
  minWidth?: boolean
  itemKey?: string
  sortDir?: undefined | "asc" | "desc"
}>()

const availableSortings: Array<TAvailableSorting> = [undefined, "asc", "desc"]

const emit = defineEmits<{
  (e: "sort-change", sortDir: undefined | "asc" | "desc", sortKey: string)
}>()

function nextSort(): TAvailableSorting {
  let currentIndex = availableSortings.indexOf(props.sortDir)
  if (currentIndex === -1) currentIndex = 0
  currentIndex++
  if (currentIndex > 2) currentIndex = 0
  return availableSortings[currentIndex]
}

function handleClick(e) {
  emit("sort-change", nextSort(), props.itemKey)
}
</script>

<style scoped></style>

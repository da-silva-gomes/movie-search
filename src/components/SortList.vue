<script setup lang="ts">
</script>

<template>
  <Select defaultValue="ascending">
    <SelectTrigger class="bg-background! border-gray-700! w-[272px]">
      <span class="text-foreground">Sort by name:</span>
      <SelectValue />
    </SelectTrigger>
    <SelectContent class="bg-primary text-foreground">
      <SelectGroup>
        <SelectItem value="ascending" default>
          Ascending
        </SelectItem>
        <SelectItem value="descending">
          Descending
        </SelectItem>
      </SelectGroup>
    </SelectContent>
  </Select>
</template>
<template>
  <div class="navbar-wrapper w-full">
    <div class="navbar-content flex justify-between w-full">
      <h3 class="logo uppercase text-2xl">
        <slot name="heading"></slot>
      </h3>
      <div>
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped />

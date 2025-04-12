<script setup>
import { ref, watch } from 'vue';
import NavBar from './components/NavBar.vue';
import Arrow from './components/icons/ArrowIcon.vue';
import NotificationIcon from './components/icons/NotificationIcon.vue';
import SearchWrapper from './components/SearchWrapper.vue';
import SearchInput from './components/SearchInput.vue';

let listVisible = ref(false);

const handleListRender = (boolean) => {
  listVisible.value = boolean;
}

watch(listVisible, (newValue) => {
  console.log('listVisible rendered:', newValue);
});

</script>

<template>
  <header>
    <NavBar>
      <template #heading>
        <span class="text-white font-bold">Concealed</span>
        <span class="text-red-600 ml-3">Films</span>
      </template>
      <div class="flex items-center">
        <SearchInput v-if="listVisible" :hasBackground="false" />
        <NotificationIcon />
        <div class="flex items-center">
          <!-- This should be a dropdown for profile pages / settings -->
          <div>
            <img class="w-8 h-8 rounded mr-2 object-cover" src="./assets/images/profile-picture.jpg" alt="JG">
          </div>
          <Arrow />
        </div>
      </div>
    </NavBar>
  </header>

  <main class="w-full flex flex-col items-center min-h-screen">
    <SearchWrapper @list-rendered="handleListRender" />
  </main>
</template>
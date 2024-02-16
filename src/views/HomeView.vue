<script setup lang="ts">

// component imports may or may not be needed in Nuxt
import LComp1 from '@/components/LComp1.vue';
import LComp2 from '@/components/LComp2.vue';
import LComp3 from '@/components/LComp3.vue';

// only zod should be needed to be imported
import { ref, computed } from 'vue';
import { useRoute } from 'vue-router';
import { z } from 'zod';

// gather query params
const route = useRoute()
const query = route.query;
const value = z.number().parse(query.value) ;
const name = z.string().parse(query.name) as ComponentName;

// setup state and component dictionary
const voteValue = ref<number>(value);
const componentDictionary = {
  'comp1': LComp1,
  'comp2': LComp2,
  'comp3': LComp3
};


// submit vote to server via API
async function fetchVoteValue(value: number) {
  // submit vote to server via API
}

// type for dictionary keys
type ComponentName = keyof typeof componentDictionary;


// render current component based on query param
const currentComponent = computed(() => {
  return componentDictionary[name];
});
</script>

<template>
  <div>
    <component :is="currentComponent" :value="voteValue" @submit="fetchVoteValue($event)" />
  </div>
</template>


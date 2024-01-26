<script lang="ts" setup></script>

<template>
  <UContainer>
    <div class="flex gap-6 py-3 border-b mb-4">
      <NuxtLink to="/users">Users</NuxtLink>
      <NuxtLink to="/posts">Posts</NuxtLink>
    </div>
    <slot />
  </UContainer>
</template>

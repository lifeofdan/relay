<template>
  <div>
    <div class="navbar rounded">
      <div class="flex-1">
        <a class="btn btn-ghost text-xl">Relay</a>
      </div>
      <div class="flex-none gap-4">
        <NuxtLink to="/">
          <button
            class="btn"
            :class="
              $route.name === 'index' ? 'btn-accent' : 'btn-outline btn-accent'
            "
          >
            Combo Poster
          </button>
        </NuxtLink>
        <NuxtLink to="/list">
          <button
            class="btn"
            :class="
              $route.name === 'list' ? 'btn-accent' : 'btn-outline btn-accent'
            "
          >
            List Poster
          </button>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped></style>

<template>
  <div>
    <template v-if="status === 'success'">
      <div class="message-contents">{{ motd!.text }}</div>
      <div class="message-date">
        {{
          new Date(motd!.lastUpdatedAt).toLocaleString("en-US", {
            dateStyle: "medium",
            timeStyle: "short",
          })
        }}
      </div>
    </template>
    <template v-else-if="status === 'pending'">Loading motd...</template>
    <template v-else-if="status === 'error'">
      Failed to load motd. {{ String(error) }}
    </template>
    <template v-else-if="status === 'idle'">
      Waiting for motd to start loading...
    </template>
  </div>
</template>
<script setup lang="ts">
const {
  data: motd,
  status,
  error,
} = await useFetch("/api/motd", {
  transform: ({ motd }) => motd,
});
</script>
<style scoped>
.message-contents {
  font-size: 1.2rem;
}

.message-date {
  font-style: italic;
}
</style>

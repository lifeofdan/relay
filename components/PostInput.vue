<template>
  <div>
    <label class="form-control">
      <div class="label">
        <span class="label-text">{{ postText }}</span>
      </div>
      <textarea
        v-model="text"
        class="textarea textarea-bordered h-24"
        placeholder="Write your message here..."
      ></textarea>
      <div class="label">
        <span class="label-text-alt"></span>
        <span
          class="label-text-alt"
          :class="text.length > platformLength ? 'text-red-600' : ''"
        >
          Length: {{ text.length }} / {{ platformLength }}
        </span>
      </div>
    </label>
    <div class="flex justify-end mt-2">
      <div>
        <button @click="submitPost" class="btn btn-primary">Post</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{ platform: TPlatform }>();
const { platform } = toRefs(props);

const text = ref("");
const postText = computed((): string => {
  switch (platform.value) {
    case "all":
      return "Post to all platforms";
    case "facebook":
      return "Post to FaceBook";
    case "instagram":
      return "Post to Instagram";
    case "x":
      return "Post to X";
    default:
      return "";
  }
});

const platformLength = computed((): number => {
  switch (platform.value) {
    case "all":
      return 280;
    case "facebook":
      return 63206;
    case "instagram":
      return 2200;
    case "x":
      return 280;
    default:
      return 0;
  }
});

async function submitPost() {
  const platformResponses: { platform: TPlatform; response: string }[] = [];

  if (platform.value === "facebook" || platform.value === "all") {
    const response = await $fetch("/api/facebook");
    platformResponses.push({
      platform: platform.value,
      response: response ?? ""
    });
  }

  if (platform.value === "instagram" || platform.value === "all") {
    const response = await $fetch("/api/instagram");
    platformResponses.push({
      platform: platform.value,
      response: response ?? ""
    });
  }

  if (platform.value === "x" || platform.value === "all") {
    const response = await $fetch("/api/x");
    platformResponses.push({
      platform: platform.value,
      response: response ?? ""
    });
  }

  console.log("responses: ", platformResponses);
}
</script>

<style scoped></style>

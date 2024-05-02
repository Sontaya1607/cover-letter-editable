<script setup lang="ts">
import { ref } from 'vue'

interface ModelState {
  you: {
    name: string
  }
  job: {
    title: string
    company: string
    source: string
    hiringManager: string
  }
}

const state = ref<ModelState>({
  you: {
    name: '',
  },
  job: {
    title: '',
    company: '',
    source: '',
    hiringManager: '',
  },
})
const isSubmitting = ref(false)

function displayState(value: string) {
  return value.length ? value : '______'
}

function handleSubmit() {
  isSubmitting.value = true
}

function handleReset() {
  state.value = {
    you: {
      name: '',
    },
    job: {
      title: '',
      company: '',
      source: '',
      hiringManager: '',
    },
  }
  isSubmitting.value = false
}
</script>

<template>
  <main class="font-nunito min-h-screen p-8 space-y-6 mx-auto container">
    <h1
      class="text-4xl text-center font-bold"
    >
      📝 Cover Letter - Editable
    </h1>

    <div class="flex flex-col lg:flex-row gap-4">
      <div class="order-1 lg:order-2 card bg-base-100 shadow-xl w-full">
        <div class="card-body space-y-4 text-base-content/60">
          <h3 class="font-semibold">
            Subject: Introduction and expression of interest in <span class="text-base-content font-bold">{{ displayState(state.job.title) }}</span> at <span class="text-base-content font-bold">{{ displayState(state.job.company) }}</span>
          </h3>

          <span>Dear <span class="text-base-content font-bold">{{ displayState(state.job.hiringManager) }}</span>,</span>

          <span>I hope this email finds you well. My name is <span class="text-base-content font-bold">{{ displayState(state.you.name) }}</span>, and I came across the <span class="text-base-content font-bold">{{ displayState(state.job.title) }}</span> position at <span class="text-base-content font-bold">{{ displayState(state.job.company) }}</span> on <span class="text-base-content font-bold">{{ displayState(state.job.source) }}</span>.</span>

          <span>Paragraph 2</span>

          <span>
            I have attached my resume for your review, and I would be honored to have the opportunity to discuss my qualifications further. I understand that your time is valuable, and I am available for an interview at your convenience.
          </span>

          <span>
            Thank you for your time and consideration. I look forward to the opportunity to further discuss my qualifications and how I can contribute to the success of <span class="text-base-content font-bold">{{ state.job.company }}</span>.
          </span>

          <div>Sincerely,</div>
          <div><span class="text-base-content font-bold">{{ displayState(state.you.name) }}</span></div>
        </div>
      </div>

      <div class="order-2 lg:order-1 card bg-base-100 shadow-xl w-full">
        <form
          class="card-body"
          @submit.prevent="handleSubmit"
          @reset.prevent="handleReset"
        >
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <h6 class="font-bold text-xl">
                You:
              </h6>
              <div class="font-control">
                <div class="label">
                  <span class="label-text">Name</span>
                </div>
                <input
                  v-model.trim="state.you.name"
                  type="text"
                  placeholder="Type your name"
                  class="input input-bordered w-full"
                  :disabled="isSubmitting"
                >
              </div>
            </div>

            <div>
              <h6 class="font-bold text-xl mt-4 md:mt-0">
                Job:
              </h6>
              <div class="font-control">
                <div class="label">
                  <span class="label-text">Title</span>
                </div>
                <input
                  v-model.trim="state.job.title"
                  type="text"
                  placeholder="Type job title"
                  class="input input-bordered w-full"
                  :disabled="isSubmitting"
                >
              </div>
              <div class="font-control">
                <div class="label">
                  <span class="label-text">Company</span>
                </div>
                <input
                  v-model.trim="state.job.company"
                  type="text"
                  placeholder="Type company name"
                  class="input input-bordered w-full"
                  :disabled="isSubmitting"
                >
              </div>
              <div class="font-control">
                <div class="label">
                  <span class="label-text">Source</span>
                </div>
                <input
                  v-model.trim="state.job.source"
                  type="text"
                  placeholder="Type source"
                  class="input input-bordered w-full"
                  :disabled="isSubmitting"
                >
              </div>
              <div class="font-control">
                <div class="label">
                  <span class="label-text">Hiring Manager</span>
                </div>
                <input
                  v-model.trim="state.job.hiringManager"
                  type="text"
                  placeholder="Type hiring manager name"
                  class="input input-bordered w-full"
                  :disabled="isSubmitting"
                >
              </div>

              <div class="flex justify-end gap-4 mt-4">
                <button type="reset" class="btn">
                  <svg class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path fill="currentColor" d="M18 28A12 12 0 1 0 6 16v6.2l-3.6-3.6L1 20l6 6l6-6l-1.4-1.4L8 22.2V16a10 10 0 1 1 10 10Z" /></svg>
                  <span>Resets</span>
                </button>
                <button
                  type="submit"
                  class="btn btn-primary"
                  :disabled="isSubmitting"
                >
                  <svg class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path fill="currentColor" d="m27.71 9.29l-5-5A1 1 0 0 0 22 4H6a2 2 0 0 0-2 2v20a2 2 0 0 0 2 2h20a2 2 0 0 0 2-2V10a1 1 0 0 0-.29-.71M12 6h8v4h-8Zm8 20h-8v-8h8Zm2 0v-8a2 2 0 0 0-2-2h-8a2 2 0 0 0-2 2v8H6V6h4v4a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V6.41l4 4V26Z" /></svg>
                  <span>Submit</span>
                </button>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>
  </main>
</template>

<template>
  <layout title="Create Organization">
    <h1 class="mb-8 font-bold text-3xl">
      <inertia-link class="text-indigo-light hover:text-indigo-dark" :href="route('organizations')">Organizations</inertia-link>
      <span class="text-indigo-light font-medium">/</span> Create
    </h1>
    <div class="bg-white rounded shadow overflow-hidden max-w-lg">
      <form @submit.prevent="submit">
        <div class="p-8 -mr-6 -mb-8 flex flex-wrap">
          <text-input v-model="form.name" :errors="errors.name" class="pr-6 pb-8 w-full lg:w-1/2" label="Name" />
          <text-input v-model="form.email" :errors="errors.email" class="pr-6 pb-8 w-full lg:w-1/2" label="Email" />
          <text-input v-model="form.phone" :errors="errors.phone" class="pr-6 pb-8 w-full lg:w-1/2" label="Phone" />
          <text-input v-model="form.address" :errors="errors.address" class="pr-6 pb-8 w-full lg:w-1/2" label="Address" />
          <text-input v-model="form.city" :errors="errors.city" class="pr-6 pb-8 w-full lg:w-1/2" label="City" />
          <text-input v-model="form.region" :errors="errors.region" class="pr-6 pb-8 w-full lg:w-1/2" label="Province/State" />
          <select-input v-model="form.country" :errors="errors.country" class="pr-6 pb-8 w-full lg:w-1/2" label="Country">
            <option :value="null" />
            <option value="CA">Canada</option>
            <option value="US">United States</option>
          </select-input>
          <text-input v-model="form.postal_code" :errors="errors.postal_code" class="pr-6 pb-8 w-full lg:w-1/2" label="Postal code" />
        </div>
        <div class="px-8 py-4 bg-grey-lightest border-t border-grey-lighter flex justify-end items-center">
          <loading-button :loading="sending" class="btn-indigo" type="submit">Create Organization</loading-button>
        </div>
      </form>
    </div>
  </layout>
</template>

<script>
import Layout from '@/Shared/Layout'
import LoadingButton from '@/Shared/LoadingButton'
import SelectInput from '@/Shared/SelectInput'
import TextInput from '@/Shared/TextInput'

export default {
  components: {
    Layout,
    LoadingButton,
    SelectInput,
    TextInput,
  },
  props: {
    errors: {
      type: Object,
      default: () => ({}),
    },
  },
  remember: ['form'],
  data() {
    return {
      sending: false,
      form: {
        name: null,
        email: null,
        phone: null,
        address: null,
        city: null,
        region: null,
        country: null,
        postal_code: null,
      },
    }
  },
  methods: {
    submit() {
      this.sending = true
      this.$inertia.post(this.route('organizations.store'), this.form)
        .then(() => this.sending = false)
    },
  },
}
</script>

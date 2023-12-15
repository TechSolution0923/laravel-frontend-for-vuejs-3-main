<script setup lang="ts">
  import { RegisterPayload } from '@/types';
  import type { FormKitNode } from '@formkit/core';
  import { handleInvalidForm } from '~~/utils';

  definePageMeta({
    layout: "centered",
    middleware: ["guest"]
  });

  const { register } = useAuth();

  async function handleRegister(payload: RegisterPayload, node?: FormKitNode) {
    try {
      await register(payload);
    } catch (error) {
      handleInvalidForm(error, node);
    }
  }
</script>
<template>
  <div class="register">
    <h1>Register</h1>
    <FormKit type="form" submit-label="register" @submit="handleRegister">
      <FormKit type="text" label="name" name="name"></FormKit>
      <FormKit type="email" label="email" name="email"></FormKit>
      <FormKit type="password" label="password" name="password"></FormKit>
      <FormKit type="password" label="password_confirmation" name="password_confirmation"></FormKit>
    </FormKit>

    <p>
      Already have an account?
      <NuxtLink class="underline text-lime-600" to="/login">Login</NuxtLink>
    </p>
  </div>
</template>

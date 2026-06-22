<script setup lang="ts">
import { isVNode } from "vue"
import { CheckCircle2 } from "lucide-vue-next"
import { Toast, ToastClose, ToastDescription, ToastProvider, ToastTitle, ToastViewport } from "."
import { useToast } from "./use-toast"

const { toasts } = useToast()
</script>

<template>
  <ToastProvider>
    <Toast v-for="toast in toasts" :key="toast.id" v-bind="toast">
      <div class="flex items-start gap-3 w-full">
        <CheckCircle2 v-if="toast.variant === 'success'" class="h-5 w-5 text-green-600 mt-0.5 shrink-0" />
        <div class="grid gap-1">
          <ToastTitle v-if="toast.title">
            {{ toast.title }}
          </ToastTitle>
          <template v-if="toast.description">
            <ToastDescription v-if="isVNode(toast.description)">
              <component :is="toast.description" />
            </ToastDescription>
            <ToastDescription v-else>
              {{ toast.description }}
            </ToastDescription>
          </template>
        </div>
      </div>
      <ToastClose />
      <component :is="toast.action" />
    </Toast>
    <ToastViewport />
  </ToastProvider>
</template>

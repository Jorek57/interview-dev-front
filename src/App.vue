<script setup>
import { useRegisterSW } from 'virtual:pwa-register/vue'

import ReloadPrompt from '@/components/ReloadPrompt.vue'

const serviceTitle = 'Interview Data.gouv'
const serviceDescription = 'Kevin Cluzel - Front End'
const logoText = ['République', 'Française']

const quickLinks = [
  {
    label: 'Home',
    to: '/',
    icon: 'ri-home-4-line',
    iconAttrs: { color: 'var(--red-marianne-425-625)' },
  },
  {
    label: 'List',
    to: '/list',
    icon: 'ri-file-pdf-line',
    iconAttrs: { color: 'var(--red-marianne-425-625)' },
  },
  {
    label: 'Register',
    to: '/register',
    icon: 'ri-account-circle-line',
    iconAttrs: { color: 'var(--red-marianne-425-625)' },
  }
]

const {
  offlineReady,
  needRefresh,
  updateServiceWorker,
} = useRegisterSW()

const close = () => {
  offlineReady.value = false
  needRefresh.value = false
}
</script>

<template>
  <DsfrHeader
    :service-title="serviceTitle"
    :service-description="serviceDescription"
    :logo-text="logoText"
    :quick-links="quickLinks"
  />

  <div class="fr-container  fr-mt-3w  fr-mt-md-5w  fr-mb-5w">
    <router-view />
  </div>
  <ReloadPrompt
    :offline-ready="offlineReady"
    :need-refresh="needRefresh"
    @close="close()"
    @update-service-worker="updateServiceWorker()"
  />
</template>

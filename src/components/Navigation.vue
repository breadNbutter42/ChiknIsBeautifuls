<script setup>
import useUser from '@/composables/useUser'
import { sliceAddress } from '@/utils'

const { isAuthenticated, isAppNetwork, isAuthenticating, login, logout, wallet, address, ens, chainName } = useUser()
</script>

<template>
  <div class="sticky top-0 z-10 h-16 px-6 backdrop-blur border-b border-white/10">
    <div class="flex items-center justify-between h-full">
      <div class="flex items-center justify-end flex-1 gap-4">
        <div v-if="isAuthenticated">
          <div class="text-sm font-semibold text-white text-right">
            {{ ens ?? sliceAddress(address) }}
          </div>
          <div class="flex items-center justify-end gap-2 text-xs text-white text-right whitespace-nowrap">
            {{ chainName }}
          </div>
        </div>
        <Button
          @click="isAuthenticated ? logout() : login()" 
          :disabled="isAuthenticating || !wallet || !isAppNetwork"
          :loading="isAuthenticating"
        >
          {{ wallet ? isAppNetwork ? isAuthenticated ? 'Logout' : 'Connect Wallet' : 'Wrong Network' : 'Unable to detect Ethereum provider' }}
        </Button>
      </div>
    </div>
  </div>
</template>

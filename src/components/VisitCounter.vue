<script setup>
import { onMounted, ref } from 'vue'
import { createClient } from '@supabase/supabase-js'

const visitCount = ref(null)
const errorMessage = ref('')
const hasError = ref(false)

onMounted(async () => {
    const url = import.meta.env.VITE_SUPABASE_URL
    const anonKey = import.meta.env.VITE_SUPABASE_ANON_KEY

    if (!url || !anonKey) {
        // errorMessage.value = 'there is a configuration error with the visit counter.'
        hasError.value = true
        console.error('Visit counter is not configured. Set the Supabase Vite environment variables.')
        return
    }

    try {
        const supabase = createClient(url, anonKey)
        const { data, error } = await supabase.rpc('increment_site_visits')

        if (error) {
            // errorMessage.value = 'there is a configuration error with the visit counter.'
            hasError.value = true
            console.error('Could not update the visit counter:', error)
            return
        }

        visitCount.value = data
    } catch (error) {
        // errorMessage.value = 'there is a configuration error with the visit counter.'
        hasError.value = true
        console.error('Could not update the visit counter:', error)
    }
})
</script>

<template>
    <p class="fixed bottom-4 right-4 z-50 m-0 rounded bg-black/80 px-3 py-2 text-right font-mono text-xs text-green-400/70">
        <span v-if="visitCount !== null">visits: {{ visitCount }}</span>
        <!-- <span v-else-if="errorMessage">{{ errorMessage }}</span> -->
        <span v-else-if="hasError">An error occurred while updating the visit counter.</span>
        <span v-else>loading visits...</span>
    </p>
</template>

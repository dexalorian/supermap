<script setup>
import { Button } from './components/ui/button';
import { DialogContent, Dialog, DialogHeader } from './components/ui/dialog';
import { useRouter } from 'vue-router';
import { ref, watch } from 'vue'
import { useUser, useMyPhotos } from './main';


const userObj = useUser()
const myPhotos = useMyPhotos()

const router = useRouter()

const props = defineProps({ show: Boolean })

const open = ref(false)

watch( () => props.show, () => open.value = props.show )


async function GlobalLogout() {
    await fetch(import.meta.env.VITE_BASE_URL+'/logout', { method: 'POST', credentials: 'include' } )

    userObj.reset()
    router.push('/')
    open.value = false
    

}


</script>

<template>

    <Dialog v-model:open="open" @update:open="() => router.push('/')">

            <DialogContent >
                <DialogHeader>Are your sure?</DialogHeader>
                <Button @click="GlobalLogout">Logout</Button>
            </DialogContent>

    </Dialog>

</template>


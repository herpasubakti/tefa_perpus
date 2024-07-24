<template>
    <div class="container-fluid">
        <div v-if="loading" class="d-flex justify-content-center">
            <div class="loader">LODING.......</div>
        </div>
        <div v-else>
            <table style="margin-left: 2%;">
                <tr class="text-center">
                    <td colspan="4">
                        <h1 style="font-family: inter"> DETAIL BUKU</h1>
                    </td>
                </tr>
                <tr>
                    <td rowspan="7"><img :src="Buku.cover" class="cover" alt="cover" /></td>
                </tr>
                <tr>
                    <td class="ps-5">JUDUL</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.judul }}</td>
                </tr>
                <tr>
                    <td class="ps-5">PENULIS</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.penulis }}</td>
                </tr>
                <tr>
                    <td class="ps-5">PENERBIT</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.penerbit }}</td>
                </tr>
                <tr>
                    <td class="ps-5">KATEGORI</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.kategori.nama }}</td>
                </tr>
                <tr>
                    <td class="ps-5">RAK</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.rak}}</td>
                </tr>
                <tr>
                    <td class="ps-5">DESKRIPSI</td>
                    <td class="ps-3">:</td>
                    <td class="ps-3">{{ Buku.deskripsi }}</td>
                </tr>
                <tr colspan="4">
                    <td style="padding-left:2%;">
                        <nuxt-link to="../buku">
                            <div class="input-group text-center mt-4 ">
                                <button type="button" class="btn btn-outline-primary rounded-4 ">
                                    back
                                </button>
                            </div>
                        </nuxt-link>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>


<script setup>
const supa = useSupabaseClient()
const route = useRoute()
const Buku = ref({})
const loading = ref(true)

const getBookById = async () => {
    loading.value = true
    const { data, error } = await supa.from('Buku').select(`*, kategori(nama)`)
        .eq('id', route.params.id)
    if (data) {
        Buku.value = data[0]
        loading.value = false
    }
}

onMounted(() => {
    getBookById()
})
</script>
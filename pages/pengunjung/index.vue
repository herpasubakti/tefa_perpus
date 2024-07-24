<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-22">
                <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
                
                <table class="table">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>nama</td>
                            <td>keanggotaan</td>
                            <td>keperluan</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(visitor,i) in visitors" :key="i">
                            <td>{{ i+1 }}</td>
                            <td>{{ visitor.nama }}</td>
                            <td>{{ visitor.keanggotaan.nama }}.</td>
                            <td>{{ visitor.keperluan.nama }}.</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
    <nuxt-link to="/">
                            <div class="input-group text-center mt-4 ">
                                <button type="button" class="btn btn-outline-primary rounded-4 ">
                                    back
                                </button>
                            </div>
                        </nuxt-link>
</template>


<script setup>

const supabase = useSupabaseClient()
const visitors = ref([])

const getPengunjung = async () =>{
    const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    if(data) visitors.value = data
}
onMounted(() =>{
    getPengunjung()
})

</script>

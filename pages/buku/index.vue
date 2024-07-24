<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-tg-12">
                <h2 class="text-center my-4">BUKU</h2>
                <form @submit.prevent="getBooks">
          <div class="my-3">
            <input v-model="keyword" type="search" class="form-control rounded-5"
              placeholder="Mau baca apa hari ini?" />
          </div>
        </form>
                <div class="my-3 text-muted"> menampilkan 3 dari 3</div>
                <div class="row">
                    <div v-for="(book, i) in books" :key="i" class="col-2">
                        <div class="card mb-3">
                            <div class="card-body">
                                <nuxt-link :to="`buku/${book.id}`">
                                    <img :src="book.cover" class="cover" alt="cover" />
                                </nuxt-link>
                            </div>
                        </div>
                    </div>

                </div>
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
const books = ref([])
const keyword = ref('')
const book=ref(0)
const getBooks = async () => {
  const { data, error } = await supabase.from('Buku').select(`*`)
    .ilike('judul', `%${keyword.value}%`)
    if(data) books.value = data
}
const hitungData = async() => {
  const { data, count } = await supabase.from("Buku").select("*", { count : 'exact'})
  if (data) book.value = count

}
onMounted(() => {
  hitungData()
  getBooks()
})

</script>
<style>
.cover {
    width: 100px;
    height: 150px;
}
</style>
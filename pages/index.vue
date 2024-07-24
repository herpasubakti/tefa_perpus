<template>
    <div class="container-fluid">
        <div class="row my-5">
            <div class="col-lg-6">
                <nuxt-link to="/pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5">
                        <div class="card-body">
                            <h2>pengunjung</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>

            <div class="col-lg-6">
                <nuxt-link to="/buku">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                            
                            <h2>cari buku</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
        <div class="row my-5">
            <div class="col-lg-6">
                    <div class="card bg-pengujubg rounded-5">
                        <div class="card-body">
                            <h1>{{ visitor }}</h1>
                            <h2>pengunjung</h2>
                        </div>
                    </div>
            </div>

            <div class="col-lg-6">
                    <div class="card bg-byku rounded-5">
                        <div class="card-body">
                            <h1>{{ book }}</h1>
                            <h2>cari buku</h2>
                        </div>
                    </div>
            </div>
        </div>
    </div>
</template>

<script setup>
useHead({ title: "Home / Perpus Digital" });
const supabase = useSupabaseClient();
const visitor = ref(0);
const book = ref(0);

const countVisitor = async () => {
  const { data, count } = await supabase
    .from("pengunjung")
    .select("*", { count: "exact" });
  if (data) visitor.value = count;
};

const countBook = async () => {
  const { data, count } = await supabase
    .from("Buku")
    .select("*", { count: "exact" });
  if (data) book.value = count;
};

onMounted(() => {
  countVisitor();
  countBook();
});
</script>

<style scoped>
.card {
    height: 250px;
    box-shadow: 1px 1px 10px #424242;
}
.card.bg-buku{
    background: url('../assets/img/bg-home-cari-buku.jpg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
.card.bg-pengunjung{
    background: url('../assets/img/bg-home-kunjungan.jpeg') no-repeat center center;
    background-size: cover;
}
.card.card.bg-pengujubg {
    background-color: grey;
}
.card.card.bg-byku{
    background-color: rgb(136, 25, 25);
}
</style>
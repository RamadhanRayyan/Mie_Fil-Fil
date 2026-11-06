<script setup lang="ts">
const menus = reactive([
  {
    id: 0,
    image: "",
    title: "Mie Nyemek",
    description:
      "Mie Nyemek adalah salah satu jenis mie yang memiliki tekstur lembut dan kenyal. Mie ini biasanya dimasak dengan kuah yang gurih dan bumbu yang kaya rasa, sehingga memberikan sensasi makan yang lezat.",
    price: 15000,
    category: "Makanan",
  },
  {
    id: 1,
    image: "",
    title: "Mie Kocok",
    description:
      "Mie Kocok adalah salah satu jenis mie yang memiliki tekstur lembut dan kenyal. Mie ini biasanya dimasak dengan kuah yang gurih dan bumbu yang kaya rasa, sehingga memberikan sensasi makan yang lezat.",
    price: 11000,
    category: "Makanan",
  },
  {
    id: 2,
    image: "",
    title: "Mie lanta",
    description:
      "Mie lanta adalah salah satu jenis mie yang memiliki tekstur lembut dan kenyal. Mie ini biasanya dimasak dengan kuah yang gurih dan bumbu yang kaya rasa, sehingga memberikan sensasi makan yang lezat.",
    price: 20000,
    category: "Obat",
  },
]);

const search = ref("");
const categoryFilter = ref("All");

const categories = computed(() => [
  { label: "semua", value: "All" },
  ...Array.from(new Set(menus.map((menu) => menu.category))).map(
    (category) => ({
      label: category,
      value: category,
    }),
  ),
]);
const filteredMenu = computed(() => {
  return menus.filter((menu) => {
    const matchesSearch = menu.title
      .toLowerCase()
      .includes(search.value.toLowerCase());
    const matchesCategory =
      categoryFilter.value === "All" || menu.category === categoryFilter.value;
    return matchesSearch && matchesCategory;
  });
});
</script>

<template>
  <UContainer>
    <UPageCTA
      title="Mie Fil Fil"
      description="Mie Fil Fil adalah salah satu jenis mie yang memiliki tekstur lembut dan kenyal. Mie ini biasanya dimasak dengan kuah yang gurih dan bumbu yang kaya rasa, sehingga memberikan sensasi makan yang lezat."
      variant="outline"
      class="my-5"
    >
      <template #links>
        <UInput v-model="search" placeholder="Cari menu..." class="w-fit" />
        <USelect
          placeholder="Pilih kategori"
          v-model="categoryFilter"
          class="w-35"
          :items="categories"
        />
      </template>
    </UPageCTA>

    <UBlogPosts>
      <UBlogPost
        v-for="menu in filteredMenu"
        :key="menu.id"
        :title="menu.title"
        :description="menu.description"
        :image="menu.image"
      >
        <template #badge>
          <div class="flex gap-x-4">
            <UBadge :label="menu.category" />
            <p class="text-primary font-semibold">Rp.{{ menu.price }}</p>
          </div>
        </template>
      </UBlogPost>
    </UBlogPosts>
  </UContainer>
</template>

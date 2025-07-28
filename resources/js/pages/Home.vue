<template>
    <body class="bg-black text-white">
    <div id="app" v-cloak>
        <Navbar />
        <!-- Categories -->
        <section class="py-6 px-4">
            <div class="flex space-x-4 overflow-x-auto">
                <button
                    v-for="category in categories"
                    :key="category"
                    @click="selectedCategory = category"
                    :class="selectedCategory === category ? 'bg-purple-600' : 'bg-gray-800'"
                    class="px-4 py-2 rounded-full whitespace-nowrap text-sm font-medium hover:bg-purple-500 transition-colors"
                >
                    {{ category }}
                </button>
            </div>
        </section>

        <!-- Products Grid -->
        <section class="px-4 pb-20">
            <h2 class="text-2xl font-bold mb-6">Популярные товары</h2>
            <div class="grid grid-cols-2 gap-4">
                <div
                    v-for="product in filteredProducts"
                    :key="product.id"
                    class="bg-gray-900 rounded-xl overflow-hidden border border-gray-800 hover:border-purple-500 transition-colors"
                >
                    <!-- Product Image -->
                    <div class="aspect-square bg-gray-800 relative overflow-hidden">
                        <img
                            :src="product.image"
                            :alt="product.name"
                            class="w-full h-full object-cover hover:scale-105 transition-transform duration-300"
                        >
                        <div class="absolute top-2 right-2">
                            <span v-if="product.isNew" class="bg-green-500 text-xs px-2 py-1 rounded-full">NEW</span>
                            <span v-if="product.isHot" class="bg-red-500 text-xs px-2 py-1 rounded-full ml-1">HOT</span>
                        </div>
                    </div>

                    <!-- Product Info -->
                    <div class="p-4">
                        <h3 class="font-semibold text-sm mb-1 line-clamp-2">{{ product.name }}</h3>
                        <p class="text-gray-400 text-xs mb-2">{{ product.brand }}</p>
                        <div class="flex items-center justify-between">
                            <span class="text-purple-400 font-bold">{{ product.price }}₽</span>
                            <button
                                @click="addToCart(product)"
                                class="bg-purple-600 text-white p-2 rounded-lg hover:bg-purple-500 transition-colors"
                            >
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"></path>
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <BottomNavbar />
    </div>
    </body>
</template>

<script>
import BottomNavbar from "../components/BottomNavbar.vue";
import Navbar from "../components/Navbar.vue";

export default {
    components: {Navbar, BottomNavbar},
    data() {
        return {
            cartCount: 3,
            selectedCategory: 'Все',
            categories: ['Все', 'Вейпы', 'Под-системы', 'Жидкости', 'Аксессуары'],
            products: [
                {
                    id: 1,
                    name: 'JUUL2 Starter Kit',
                    brand: 'JUUL',
                    price: 4500,
                    image: 'https://drsmoke.org/image/cache/catalog/poddev/drag-x2/241124_0144_dsc09529-900x1200.jpg',
                    category: 'Под-системы',
                    isNew: true,
                    isHot: false
                },
                {
                    id: 2,
                    name: 'IQOS ILUMA Prime',
                    brand: 'IQOS',
                    price: 8900,
                    image: 'https://1табачный.online/upload/dev2fun.imagecompress/webp/iblock/d17/n5mmjphmv5yfdqse2oce9czbj93j8d0t.webp',
                    category: 'Вейпы',
                    isNew: false,
                    isHot: true
                },
                {
                    id: 3,
                    name: 'Vaporesso XROS 3',
                    brand: 'Vaporesso',
                    price: 2800,
                    image: 'https://vapebarmarket.com/img/39990/HQD6/440x440,r/hqd-cuvie-plus-1200-puffs-blueberry-raspberry-disposable-pod-vape-20mg.webp?time=1689247255',
                    category: 'Под-системы',
                    isNew: false,
                    isHot: false
                },
                {
                    id: 4,
                    name: 'Пинк Лимонад 30мл',
                    brand: 'CloudLab',
                    price: 650,
                    image: 'https://drvaper.com/wp-content/uploads/2023/06/Elf-bar-Rainbow-Candy-5000puffs-500x500.jpg.webp',
                    category: 'Жидкости',
                    isNew: true,
                    isHot: false
                },
                {
                    id: 5,
                    name: 'Lost Vape Orion Bar',
                    brand: 'Lost Vape',
                    price: 1200,
                    image: 'https://images.unsplash.com/photo-1565867808626-7da516f6c4dd?w=300&h=300&fit=crop&seed=5',
                    category: 'Вейпы',
                    isNew: false,
                    isHot: true
                },
                {
                    id: 6,
                    name: 'Зарядное устройство USB-C',
                    brand: 'Universal',
                    price: 450,
                    image: 'https://images.unsplash.com/photo-1583394838336-acd977736f90?w=300&h=300&fit=crop',
                    category: 'Аксессуары',
                    isNew: false,
                    isHot: false
                }
            ]
        };
    },
    computed: {
        filteredProducts() {
            if (this.selectedCategory === 'Все') {
                return this.products;
            }
            return this.products.filter(product => product.category === this.selectedCategory);
        }
    },
};
</script>

<style scoped>
[v-cloak] {
    display: none;
}
body {
    background-color: #000;
}
.gradient-ghost {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
</style>

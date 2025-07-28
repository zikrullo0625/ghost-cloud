<template>
    <header class="bg-gray-900 border-b border-gray-800 sticky top-0 z-50">
        <div class="flex items-center justify-between p-4">
            <!-- Burger Menu -->
            <button
                @click="toggleMenu"
                class="p-2 hover:bg-gray-800 rounded-lg transition-colors md:hidden"
            >
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                        v-if="!isMenuOpen"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M4 6h16M4 12h16M4 18h16"
                    ></path>
                    <path
                        v-else
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M6 18L18 6M6 6l12 12"
                    ></path>
                </svg>
            </button>

            <!-- Logo -->
            <div class="flex items-center space-x-2">
                <img class="w-7 h-9" src="../../files/logo.png" />
                <span class="text-xl font-bold text-white">GhostClouds</span>
            </div>

            <!-- Cart -->
            <button class="p-2 hover:bg-gray-800 rounded-lg transition-colors relative">
                <i class="w-6 h-6 fa-solid fa-cart-shopping text-white"></i>
                <span
                    class="absolute -top-1 -right-1 bg-purple-600 text-xs rounded-full w-5 h-5 flex items-center justify-center"
                >
          {{ cartCount }}
        </span>
            </button>
        </div>

        <!-- Mobile Dropdown -->
        <transition name="menu-transition">
            <div
                v-show="isMenuOpen"
                class="overflow-hidden bg-gray-800 border-t border-gray-700 md:hidden"
                ref="menuRef"
            >
                <nav class="p-4 space-y-3">
                    <a
                        v-for="link in links"
                        :key="link"
                        href="#"
                        class="block py-2 px-3 rounded-lg hover:bg-gray-700 transition-colors text-white"
                    >
                        {{ link }}
                    </a>
                </nav>
            </div>
        </transition>
    </header>
</template>

<script>
export default {
    data() {
        return {
            isMenuOpen: false,
            cartCount: 3,
            links: ["Главная", "Вейпы", "Жидкости", "Аксессуары", "О нас", "Контакты"],
        };
    },
    methods: {
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
        },
    },
};
</script>

<style scoped>
.menu-transition-enter-active,
.menu-transition-leave-active {
    transition: max-height 0.3s ease, opacity 0.3s ease;
}
.menu-transition-enter-from,
.menu-transition-leave-to {
    max-height: 0;
    opacity: 0;
}
.menu-transition-enter-to,
.menu-transition-leave-from {
    max-height: 400px;
    opacity: 1;
}
</style>

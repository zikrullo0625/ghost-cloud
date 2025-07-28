<script>
import axios from 'axios'
export default {
    data() {
        return {
            email: '',
            password: '',
            rememberMe: false,
            showPassword: false,
            isLoading: false,
            showToast: false,
            toastMessage: ''
        };
    },
    methods: {
        async login() {
            if (!this.email || !this.password) {
                this.showToastMessage('Пожалуйста, заполните все поля');
                return;
            }

            this.isLoading = true;

            await axios.post('/api/auth/email', {
                email: this.email,
                password: this.password
            })
            .then(response => {

            });
        },
        async loginWithGoogle() {
            this.showToastMessage('Переход к авторизации Google...');
            console.log('Вход через Google');
            // Здесь будет логика для Google OAuth
        },
        async loginWithTelegram() {
            this.showToastMessage('Переход к авторизации Telegram...');
            console.log('Вход через Telegram');
            // Здесь будет логика для Telegram Login Widget
        },
        showToastMessage(message) {
            this.toastMessage = message;
            this.showToast = true;
            setTimeout(() => {
                this.showToast = false;
            }, 3000);
        }
    }
};
</script>


<template>
    <body class="gradient-bg min-h-screen text-white">
    <div id="app" v-cloak class="min-h-screen">
        <!-- Login Form Container -->
        <div class="flex items-center justify-center px-4 pt-8 ">
            <div class="w-full max-w-md">
                <!-- Welcome Text -->
                <div class="text-center mb-8">
                    <h1 class="text-3xl font-bold mb-2">GhostClouds</h1>
                    <p class="text-gray-400">Войдите в свой аккаунт GhostClouds</p>
                </div>

                <!-- Login Form Card -->
                <div class="glass-effect rounded-2xl p-6 mb-6">
                    <div class="space-y-5">
                        <!-- Email Field -->
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">
                                Email или телефон
                            </label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                    <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor"
                                         viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                              d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                                    </svg>
                                </div>
                                <input
                                    v-model="email"
                                    type="email"
                                    class="block w-full pl-10 pr-3 py-3 bg-gray-800 border border-gray-600 rounded-xl focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent text-white placeholder-gray-400"
                                    placeholder="Введите email или телефон"
                                >
                            </div>
                        </div>

                        <!-- Password Field -->
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">
                                Пароль
                            </label>
                            <div class="relative">
                                <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                    <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor"
                                         viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                              d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path>
                                    </svg>
                                </div>
                                <input
                                    v-model="password"
                                    :type="showPassword ? 'text' : 'password'"
                                    class="block w-full pl-10 pr-12 py-3 bg-gray-800 border border-gray-600 rounded-xl focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent text-white placeholder-gray-400"
                                    placeholder="Введите пароль"
                                >
                                <button
                                    @click="showPassword = !showPassword"
                                    type="button"
                                    class="absolute inset-y-0 right-0 pr-3 flex items-center"
                                >
                                    <svg v-if="!showPassword" class="h-5 w-5 text-gray-400" fill="none"
                                         stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                              d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                              d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
                                    </svg>
                                    <svg v-else class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor"
                                         viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                              d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.878 9.878L3 3m6.878 6.878L21 21"></path>
                                    </svg>
                                </button>
                            </div>
                        </div>

                        <!-- Remember Me & Forgot Password -->
                        <div class="flex items-center justify-between">
                            <div class="flex items-center">
                                <input
                                    v-model="rememberMe"
                                    type="checkbox"
                                    class="h-4 w-4 text-purple-600 focus:ring-purple-500 border-gray-300 rounded bg-gray-800"
                                >
                                <label class="ml-2 block text-sm text-gray-300">
                                    Запомнить меня
                                </label>
                            </div>
                        </div>

                        <!-- Login Button -->
                        <button
                            @click="login"
                            :disabled="isLoading"
                            class="w-full gradient-ghost text-white py-3 px-4 rounded-xl font-semibold hover:opacity-90 transition-opacity shadow-lg disabled:opacity-50"
                        >
                            <span v-if="!isLoading">Войти</span>
                            <div v-else class="flex items-center justify-center">
                                <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
                                     xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor"
                                            stroke-width="4"></circle>
                                    <path class="opacity-75" fill="currentColor"
                                          d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                                </svg>
                                Вход...
                            </div>
                        </button>
                    </div>
                </div>

                <!-- Social Login -->
                <div class="glass-effect rounded-2xl p-6 mb-6">
                    <div class="text-center text-gray-400 text-sm mb-4">
                        Или войдите через
                    </div>

                    <div class="space-y-3">
                        <!-- Google Login -->
                        <button
                            @click="loginWithGoogle"
                            class="w-full flex items-center justify-center py-3 px-4 bg-white text-gray-800 rounded-xl hover:bg-gray-100 transition-colors font-medium"
                        >
                            <svg class="w-5 h-5 mr-3" viewBox="0 0 24 24">
                                <path fill="#4285F4"
                                      d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                                <path fill="#34A853"
                                      d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                                <path fill="#FBBC05"
                                      d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                                <path fill="#EA4335"
                                      d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
                            </svg>
                            Продолжить с Google
                        </button>

                        <!-- Telegram Login -->
                        <button
                            @click="loginWithTelegram"
                            class="w-full flex items-center justify-center py-3 px-4 bg-blue-500 text-white rounded-xl hover:bg-blue-600 transition-colors font-medium"
                        >
                            <svg class="w-5 h-5 mr-3" fill="currentColor" viewBox="0 0 24 24">
                                <path
                                    d="M11.944 0A12 12 0 0 0 0 12a12 12 0 0 0 12 12 12 12 0 0 0 12-12A12 12 0 0 0 12 0a12 12 0 0 0-.056 0zm4.962 7.224c.1-.002.321.023.465.14a.506.506 0 0 1 .171.325c.016.093.036.306.02.472-.18 1.898-.962 6.502-1.36 8.627-.168.9-.499 1.201-.82 1.23-.696.065-1.225-.46-1.9-.902-1.056-.693-1.653-1.124-2.678-1.8-1.185-.78-.417-1.21.258-1.91.177-.184 3.247-2.977 3.307-3.23.007-.032.014-.15-.056-.212s-.174-.041-.249-.024c-.106.024-1.793 1.14-5.061 3.345-.48.33-.913.49-1.302.48-.428-.008-1.252-.241-1.865-.44-.752-.245-1.349-.374-1.297-.789.027-.216.325-.437.893-.663 3.498-1.524 5.83-2.529 6.998-3.014 3.332-1.386 4.025-1.627 4.476-1.635z"/>
                            </svg>
                            Продолжить с Telegram
                        </button>
                    </div>
                </div>

            </div>
        </div>

        <!-- Success Toast -->
        <div
            v-if="showToast"
            class="fixed top-4 right-4 bg-red-600 text-white px-4 py-3 rounded-lg shadow-lg z-50 transition-all duration-300"
        >
            <div class="flex items-center">
                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd"
                          d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                          clip-rule="evenodd"></path>
                </svg>
                {{ toastMessage }}
            </div>
        </div>
    </div>
    </body>
</template>
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

.gradient-bg {
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
}

.glass-effect {
    background: rgba(31, 41, 55, 0.8);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(75, 85, 99, 0.3);
}
</style>

<template>
    <div class="header">
        <div class="header__content">
            <div class="header__content__logo">
                <div class="header__content__logo-img">
                    <img @click="$router.push('/')" src="@/assets/logo.png" alt="" style="cursor: pointer;">
                </div>
            </div>
            <nav class="header__content__navbar">
                <ul>
                    <router-link to="/" class="header__content__navbar-link">Главная</router-link>
                    <router-link to="/" class="header__content__navbar-link">Тарифы</router-link>
                    <router-link to="/" class="header__content__navbar-link">FAQ</router-link>
                </ul>
            </nav>
            <!-- if registred -->
            <div v-if="this.isLogged" class="header__content__user">
                <div class="header__content__user-info">
                    <div class="header__content__user-info__key">
                        <p>Использовано компаний:</p>
                        <p>Лимит по компаниям:</p>
                    </div>
                    <div class="header__content__user-info__value">
                        <p>{{ userCompanies.usedCompanyCount }}</p>
                        <p>{{ userCompanies.companyLimit }}</p>
                    </div>
                </div>
                <div class="header__content__user-menu">
                    <div class="header__content__user-menu__content">
                        <p>Артём П.</p>
                        <p @click="this.logOut">Выйти</p>
                    </div>
                    <div class="header__content__user-menu__avatar">
                        <img src="@/assets/avatar.jpg" alt="">
                    </div>
                </div>
            </div>
            <!-- if non registred -->
            <div v-else class="header__content__register">
                <button class="signUp">Зарегистрироваться</button>
                <hr class="signHr">
                <router-link to="/auth" class="signIn">Войти</router-link>
            </div>
        </div>
    </div>
</template>

<script>
import { useAuthStore } from '@/store/auth';
import { mapState } from 'pinia';
import { useRouter } from 'vue-router';
import MobileMenu from "@/components/MobileMenu";

export default {
    components: {
        MobileMenu,
    },
    data() {
        return {
            router: useRouter(),
            authStore: useAuthStore(),
            mobileMenuVisible: false,
            userCompanies: JSON.parse(localStorage.getItem('userCompanies'))
        }
    },
    methods: {
        showMobileMenu() {
            this.mobileMenuVisible = true;
        },
        logOut() {
            this.authStore.logOut();
            this.router.push('/')
        }
    },
    computed: {
        ...mapState(useAuthStore, {
            isLogged: 'getStatus',
        })
    }
}
</script>

<style scoped>
p {
    font-size: 18px;
    font-weight: 400;
}

.header {
    width: 100%;
    display: flex;
    justify-content: center;
}

.header__content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 93px;
    width: 1320px;
    margin: 0 20px;
}

.header__content__logo {
    display: flex;
    justify-content: flex-start;
    height: 80px;
    /* width: 30%; */
}

.header__content__logo img {
    object-fit: contain;
    width: 100%;
    height: 100%;
}

.header__content__navbar {
    width: 240px;
}

.header__content__navbar__hamburger-menu {
    display: none;
}

ul {
    display: flex;
    justify-content: space-between;
    list-style: none;
    cursor: pointer;
    margin: 0;
    padding: 0;
}

.header__content__navbar-link {
    font-weight: 400;
    font-size: 14px;
    transition: 1s;
    text-decoration: none;
    color: var(--color2);
}

.header__content__navbar-link:hover {
    font-weight: 600;
    transition: .25s;
}

.header__content__register {
    display: flex;
    justify-content: space-between;
    width: 250px;
    height: 26px;
}

.signUp {
    background: none;
    border: none;
    font-weight: 400;
    opacity: .4;
    cursor: pointer;
    transition: 1s;
}

.signUp:hover {
    opacity: 1;
    transition: .25s;
}

.signHr {
    background-color: var(--color1);
    border: none;
    width: 2px;
    margin: 0;
}

.signIn {
    background-color: var(--color5);
    color: var(--color2);
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    font-weight: 500;
    transition: 1s;
    text-decoration: none;
}

.signIn:hover {
    scale: 1.05;
    cursor: pointer;
    box-shadow: #7CE3E1 0 1px 10px;
    transition: .25s;
}

.signUp__mobile {
    display: none;
}

.signIn__mobile {
    display: none;
}

.signHr__mobile {
    display: none;
}

.header__content__navbar__mobile-menu {
    display: none;
}

.header__content__user {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 10px;
}

.header__content__user-info {
    min-width: 185px;
    height: 65px;
    background-color: #D9D9D930;
    border-radius: 8px;
    display: flex;
    align-items: center;
    padding: 5px;
    gap: 5px;
}

.header__content__user-info__key>p {
    font-size: 12px;
    opacity: .4;
}

.header__content__user-info__value>p {
    font-size: 14px;
    font-weight: 700;
}

.header__content__user-info__value>p:last-child {
    font-size: 14px;
    font-weight: 700;
    color: #8AC540;
}

.header__content__user-menu {
    display: flex;
    height: 40px;
    gap: 10px;
    min-width: 120px;
}

.header__content__user-menu__content {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-end;
}
.header__content__user-menu__content>p:first-child {
    font-size: 14px;
    opacity: .7;
}
.header__content__user-menu__content>p:last-child {
    font-size: 12px;
    opacity: .4;
    cursor: pointer;
    transition: .25s;
}

.header__content__user-menu__content>p:last-child:hover {
    opacity: 1;
    transition: .25s;
}

.header__content__user-menu__avatar{
    height: 40px;
    width: 40px;
}

.header__content__user-menu__avatar>img {
    object-fit: cover;
    width: 100%;
    height: 100%;
    border-radius: 50%;
}
/* @media screen and (max-width: 700px) {
    .header {
        position: fixed;
        background-color: #ffffff90;
        z-index: 5;
        backdrop-filter: blur(20px);
    }

    .header__content {
        position: relative;
    }

    .header__content__navbar {
        width: auto;
        cursor: pointer;
        margin-right: 10px;
    }

    .header__content__register {
        display: none;
    }

    .header__content__navbar__mobile-menu {
        display: block;
    }

    ul {
        display: none
    }
} */
</style>
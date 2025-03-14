<template>
    <div :class="landingClass">
        <AppNews />
        <AppTopBar :showConfigurator="false" :showMenuButton="false" @darkswitch-click="onDarkModeToggle" />
        <HeroSection />
        <FeaturesSection />
        <UsersSection />
        <ThemeSection :theme="tableTheme" @table-theme-change="onTableThemeChange" />
        <BlockSection />
        <TemplateSection />
        <FooterSection />
    </div>
</template>

<script>
definePageMeta({
    layout: 'custom'
});

import EventBus from '@/layouts/AppEventBus';
import AppNews from '@/layouts/AppNews';
import AppTopBar from '@/layouts/AppTopBar.vue';
import BlockSection from './landing/BlockSection';
import FeaturesSection from './landing/FeaturesSection';
import FooterSection from './landing/FooterSection';
import HeroSection from './landing/HeroSection';
import TemplateSection from './landing/TemplateSection';
import ThemeSection from './landing/ThemeSection';
import UsersSection from './landing/UsersSection';

export default {
    props: {
        theme: {
            type: String,
            default: null
        }
    },
    data() {
        return {
            tableTheme: 'lara-light-teal'
        };
    },
    themeChangeListener: null,
    mounted() {
        let afId = this.$route.query['af_id'];

        if (afId) {
            let today = new Date();
            let expire = new Date();

            expire.setTime(today.getTime() + 3600000 * 24 * 7);
            document.cookie = 'primeaffiliateid=' + afId + ';expires=' + expire.toUTCString() + ';path=/; domain:primefaces.org';
        }

        this.replaceTableTheme(this.$appState.darkTheme ? 'lara-dark-teal' : 'lara-light-teal');
    },
    methods: {
        onDarkModeToggle() {
            const newTheme = this.$appState.darkTheme ? 'lara-light-teal' : 'lara-dark-teal';
            const newTableTheme = this.$appState.darkTheme ? this.tableTheme.replace('dark', 'light') : this.tableTheme.replace('light', 'dark');

            EventBus.emit('theme-change', { theme: newTheme, dark: !this.$appState.darkTheme });
            this.replaceTableTheme(newTableTheme);
        },
        onTableThemeChange(value) {
            this.replaceTableTheme(value);
        },
        replaceTableTheme(newTheme) {
            const elementId = 'home-table-link';
            const linkElement = document.getElementById(elementId);
            const tableThemeTokens = linkElement?.getAttribute('href').split('/') || null;
            const currentTableTheme = tableThemeTokens ? tableThemeTokens[tableThemeTokens.length - 2] : null;

            if (currentTableTheme !== newTheme && tableThemeTokens) {
                const newThemeUrl = linkElement.getAttribute('href').replace(currentTableTheme, newTheme);

                const cloneLinkElement = linkElement.cloneNode(true);

                cloneLinkElement.setAttribute('id', elementId + '-clone');
                cloneLinkElement.setAttribute('href', newThemeUrl);
                cloneLinkElement.addEventListener('load', () => {
                    linkElement.remove();
                    cloneLinkElement.setAttribute('id', elementId);
                });
                linkElement.parentNode?.insertBefore(cloneLinkElement, linkElement.nextSibling);

                this.tableTheme = newTheme;
            }
        }
    },
    computed: {
        landingClass() {
            return ['landing', { 'layout-dark': this.$appState?.darkTheme, 'layout-light': !this.$appState?.darkTheme, 'layout-news-active': this.$appState?.newsActive }];
        }
    },
    components: {
        AppNews,
        AppTopBar,
        HeroSection,
        ThemeSection,
        BlockSection,
        TemplateSection,
        UsersSection,
        FeaturesSection,
        FooterSection
    }
};
</script>

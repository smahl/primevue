<template>
    <Sidebar v-model:visible="visible" @hide="onSidebarHide" :class="containerClass" position="right">
        <div class="p-2">
            <section class="pb-4 flex align-items-center justify-content-between border-bottom-1 surface-border">
                <span class="text-xl font-semibold">Scale</span>
                <div class="flex align-items-center gap-2 border-1 surface-border p-2" style="border-radius: 30px">
                    <Button icon="pi pi-minus" @click="decrementScale" text rounded class="w-2rem h-2rem" :disabled="scale === scales[0]" />
                    <i v-for="s in scales" :key="s" :class="['pi pi-circle-fill text-sm text-200', { 'text-lg text-primary': s === scale }]" />

                    <Button icon="pi pi-plus" @click="incrementScale" text rounded class="w-2rem h-2rem" :disabled="scale === scales[scales.length - 1]" />
                </div>
            </section>

            <section class="py-4 flex align-items-center justify-content-between border-bottom-1 surface-border">
                <span class="text-xl font-semibold">Input Style</span>
                <SelectButton :modelValue="inputStyle" @update:modelValue="onInputStyleChange" :options="inputStyles" optionLabel="label" optionValue="value" />
            </section>

            <section class="py-4 flex align-items-center justify-content-between border-bottom-1 surface-border">
                <span class="text-xl font-semibold">Ripple Effect</span>
                <InputSwitch :modelValue="rippleActive" @update:modelValue="onRippleChange" />
            </section>

            <section class="py-4 flex align-items-center justify-content-between border-bottom-1 surface-border">
                <span :class="['text-xl font-semibold', { 'p-disabled': darkToggleDisabled }]">Dark Mode</span>
                <InputSwitch :modelValue="darkMode" @update:modelValue="onDarkModeChange" :disabled="darkToggleDisabled" />
            </section>

            <section class="py-4 border-bottom-1 surface-border">
                <div class="text-xl font-semibold mb-3">Themes</div>
                <div class="flex align-items-center gap-2 mb-3">
                    <img src="https://primefaces.org/cdn/primevue/images/themes/lara-light-teal.png" alt="Lara Light Teal" class="border-circle" style="width: 1.5rem" />
                    <span class="font-medium">Lara</span>
                </div>
                <div class="flex align-items-center justify-content-between gap-3">
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('lara', 'teal'), 'hover:border-500 surface-border': !isThemeActive('lara', 'teal') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('lara', 'teal')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #4dac9c 0%, rgba(77, 172, 156, 0.5) 100%)"></span>
                    </button>
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('lara', 'blue'), 'hover:border-500 surface-border': !isThemeActive('lara', 'blue') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('lara', 'blue')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #4378e6 0%, rgba(67, 120, 230, 0.5) 100%)"></span>
                    </button>
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('lara', 'indigo'), 'hover:border-500 surface-border': !isThemeActive('lara', 'indigo') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('lara', 'indigo')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #585fe0 0%, rgba(88, 95, 224, 0.5) 100%)"></span>
                    </button>
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('lara', 'purple'), 'hover:border-500 surface-border': !isThemeActive('lara', 'purple') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('lara', 'purple')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #7758e4 0%, rgba(119, 88, 228, 0.5) 100%)"></span>
                    </button>
                </div>
            </section>
            <section class="py-4 border-bottom-1 surface-border">
                <div class="flex align-items-center gap-2 mb-3">
                    <img src="https://primefaces.org/cdn/primevue/images/themes/md-light-indigo.svg" alt="Material Design" class="border-circle" style="width: 1.5rem" />
                    <span class="font-medium">Material Design</span>
                    <div class="ml-auto flex align-items-center gap-2">
                        <label for="material-condensed" class="text-sm">Condensed</label>
                        <InputSwitch inputId="material-condensed" :modelValue="compactMaterial" @update:modelValue="onCompactMaterialChange" class="ml-auto" />
                    </div>
                </div>
                <div class="flex align-items-center justify-content-between gap-3">
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('md', 'indigo'), 'hover:border-500 surface-border': !isThemeActive('md', 'indigo') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('md', 'indigo')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #0565f2 0%, rgba(5, 101, 242, 0.5) 100%)"></span>
                    </button>
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('md', 'deeppurple'), 'hover:border-500 surface-border': !isThemeActive('md', 'deeppurple') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('md', 'deeppurple')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #702f92 0%, rgba(112, 47, 146, 0.5) 100%)"></span>
                    </button>
                    <div class="w-3"></div>
                    <div class="w-3"></div>
                </div>
            </section>
            <section class="py-4 border-bottom-1 surface-border">
                <div class="flex align-items-center gap-2 mb-3">
                    <img src="https://primefaces.org/cdn/primevue/images/themes/bootstrap4-light-blue.svg" alt="Bootstrap" class="border-circle" style="width: 1.5rem" />
                    <span class="font-medium">Bootstrap</span>
                </div>
                <div class="flex align-items-center justify-content-between gap-3">
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('bootstrap4', 'blue'), 'hover:border-500 surface-border': !isThemeActive('bootstrap4', 'blue') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('bootstrap4', 'blue')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #027bff 0%, rgba(2, 123, 255, 0.5) 100%)"></span>
                    </button>
                    <button
                        :class="[
                            'bg-transparent border-1 cursor-pointer p-2 w-3 flex align-items-center justify-content-center transition-all transition-duration-200',
                            { 'border-primary': isThemeActive('bootstrap4', 'purple'), 'hover:border-500 surface-border': !isThemeActive('bootstrap4', 'purple') }
                        ]"
                        style="border-radius: 30px"
                        @click="changeTheme('bootstrap4', 'purple')"
                    >
                        <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #893cae 0%, rgba(137, 60, 174, 0.5) 100%)"></span>
                    </button>
                    <div class="w-3"></div>
                    <div class="w-3"></div>
                </div>
            </section>
            <section class="py-4 border-bottom-1 surface-border">
                <div class="flex gap-3">
                    <div class="w-3">
                        <div class="flex align-items-center gap-2 mb-3">
                            <img src="https://primefaces.org/cdn/primevue/images/themes/soho-light.png" alt="Soho" class="border-circle" style="width: 1.5rem" />
                            <span class="font-medium">Soho</span>
                        </div>
                        <button
                            :class="[
                                'bg-transparent border-1 cursor-pointer p-2 w-full flex align-items-center justify-content-center transition-all transition-duration-200',
                                { 'border-primary': isThemeActive('soho'), 'hover:border-500 surface-border': !isThemeActive('soho') }
                            ]"
                            style="border-radius: 30px"
                            @click="changeTheme('soho')"
                        >
                            <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #664beb 0%, rgba(102, 75, 235, 0.5) 100%)"></span>
                        </button>
                    </div>
                    <div class="w-3">
                        <div class="flex align-items-center gap-2 mb-3">
                            <img src="https://primefaces.org/cdn/primevue/images/themes/viva-light.svg" alt="Viva" class="border-circle" style="width: 1.5rem" />
                            <span class="font-medium">Viva</span>
                        </div>
                        <button
                            :class="[
                                'bg-transparent border-1 cursor-pointer p-2 w-full flex align-items-center justify-content-center transition-all transition-duration-200',
                                { 'border-primary': isThemeActive('viva'), 'hover:border-500 surface-border': !isThemeActive('viva') }
                            ]"
                            style="border-radius: 30px"
                            @click="changeTheme('viva')"
                        >
                            <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #4a67c9 0%, rgba(74, 103, 201, 0.5) 100%)"></span>
                        </button>
                    </div>
                    <div class="w-3"></div>
                    <div class="w-3"></div>
                </div>
            </section>
            <section class="py-4">
                <div class="flex gap-3">
                    <div class="w-3">
                        <div class="flex align-items-center gap-2 mb-3">
                            <img src="https://primefaces.org/cdn/primevue/images/themes/fluent-light.png" alt="Fluent" class="border-circle" style="width: 1.5rem" />
                            <span class="font-medium">Fluent</span>
                        </div>
                        <button
                            :class="[
                                'bg-transparent border-1 cursor-pointer p-2 w-full flex align-items-center justify-content-center transition-all transition-duration-200',
                                { 'border-primary': isThemeActive('fluent-light'), 'hover:border-500 surface-border': !isThemeActive('fluent-light') }
                            ]"
                            style="border-radius: 30px"
                            @click="changeTheme('fluent-light')"
                        >
                            <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #0078d4 0%, rgba(0, 120, 212, 0.5) 100%)"></span>
                        </button>
                    </div>
                    <div class="w-3">
                        <div class="flex align-items-center gap-2 mb-3">
                            <img src="https://primefaces.org/cdn/primevue/images/themes/mira.jpg" alt="Mira" class="border-circle" style="width: 1.5rem" />
                            <span class="font-medium">Mira</span>
                        </div>
                        <button
                            :class="[
                                'bg-transparent border-1 cursor-pointer p-2 w-full flex align-items-center justify-content-center transition-all transition-duration-200',
                                { 'border-primary': isThemeActive('mira'), 'hover:border-500 surface-border': !isThemeActive('mira') }
                            ]"
                            style="border-radius: 30px"
                            @click="changeTheme('mira')"
                        >
                            <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #81a1c1 0%, rgba(129, 161, 193, 0.5) 100%)"></span>
                        </button>
                    </div>
                    <div class="w-3">
                        <div class="flex align-items-center gap-2 mb-3">
                            <img src="https://primefaces.org/cdn/primevue/images/themes/nano.jpg" alt="Nano" class="border-circle" style="width: 1.5rem" />
                            <span class="font-medium">Nano</span>
                        </div>
                        <button
                            :class="[
                                'bg-transparent border-1 cursor-pointer p-2 w-full flex align-items-center justify-content-center transition-all transition-duration-200',
                                { 'border-primary': isThemeActive('nano'), 'hover:border-500 surface-border': !isThemeActive('nano') }
                            ]"
                            style="border-radius: 30px"
                            @click="changeTheme('nano')"
                        >
                            <span class="block h-1rem w-full" style="border-radius: 30px; background: linear-gradient(180deg, #1469b4 0%, rgba(20, 105, 180, 0.5) 100%)"></span>
                        </button>
                    </div>
                    <div class="w-3"></div>
                </div>
            </section>
        </div>
    </Sidebar>
</template>

<script>
import EventBus from '@/layouts/AppEventBus';

export default {
    emits: ['updateConfigActive', 'darkswitch-click'],
    props: {
        configActive: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            visible: false,
            scale: 14,
            scales: [12, 13, 14, 15, 16],
            inputStyles: [
                { label: 'Outlined', value: 'outlined' },
                { label: 'Filled', value: 'filled' }
            ],
            compactMaterial: false,
            lightOnlyThemes: ['fluent-light', 'mira', 'nano']
        };
    },
    watch: {
        configActive(value) {
            this.visible = value;
        }
    },
    outsideClickListener: null,
    themeChangeListener: null,
    beforeUnmount() {
        EventBus.off('theme-change', this.themeChangeListener);
    },
    mounted() {
        this.themeChangeListener = (event) => {
            if (event.theme === 'nano') this.scale = 12;
            else this.scale = 14;

            this.applyScale();
        };

        EventBus.on('theme-change', this.themeChangeListener);
    },
    methods: {
        onSidebarHide() {
            this.visible = false;
            this.$emit('updateConfigActive', false);
        },
        changeTheme(theme, color) {
            let newTheme, dark;

            if (this.lightOnlyThemes.includes(theme)) {
                newTheme = theme;
                dark = false;
            } else {
                newTheme = theme + '-' + (this.$appState.darkTheme ? 'dark' : 'light');

                if (color) {
                    newTheme += '-' + color;
                }

                if (newTheme.startsWith('md-') && this.compactMaterial) {
                    newTheme = newTheme.replace('md-', 'mdc-');
                }

                dark = this.$appState.darkTheme;
            }

            EventBus.emit('theme-change', { theme: newTheme, dark: dark });
        },
        decrementScale() {
            this.scale--;
            this.applyScale();
        },
        incrementScale() {
            this.scale++;
            this.applyScale();
        },
        applyScale() {
            document.documentElement.style.fontSize = this.scale + 'px';
        },
        onInputStyleChange(value) {
            this.$primevue.config.inputStyle = value;
        },
        onRippleChange(value) {
            this.$primevue.config.ripple = value;
        },
        onDarkModeChange() {
            this.$emit('darkswitch-click');
        },
        onCompactMaterialChange(value) {
            this.compactMaterial = value;

            if (this.$appState.theme.startsWith('md')) {
                let tokens = this.$appState.theme.split('-');

                this.changeTheme(tokens[0].substring(0, 2), tokens[2]);
            }
        },
        isThemeActive(theme, color) {
            let themeName;
            let themePrefix = this.compactMaterial ? 'mdc' : theme;

            if (this.lightOnlyThemes.includes(themePrefix)) {
                themeName = themePrefix;
            } else {
                themeName = themePrefix + (this.$appState.darkTheme ? '-dark' : '-light');
            }

            if (color) {
                themeName += '-' + color;
            }

            return this.$appState.theme === themeName;
        }
    },
    computed: {
        inputStyle() {
            return this.$primevue.config.inputStyle;
        },
        darkMode() {
            return this.$appState.darkTheme;
        },
        rippleActive() {
            return this.$primevue.config.ripple;
        },
        darkToggleDisabled() {
            return this.lightOnlyThemes.includes(this.$appState.theme);
        },
        containerClass() {
            return [
                'layout-config w-full sm:w-26rem',
                {
                    'layout-dark': this.$appState.darkTheme,
                    'layout-light': !this.$appState.darkTheme
                }
            ];
        }
    }
};
</script>

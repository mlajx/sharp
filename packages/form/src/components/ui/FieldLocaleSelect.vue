<template>
    <div class="SharpFieldLocaleSelect">
        <template v-for="locale in locales">
            <button
                class="SharpFieldLocaleSelect__btn ml-2"
                :class="{
                    'SharpFieldLocaleSelect__btn--active': isActive(locale),
                    'SharpFieldLocaleSelect__btn--empty': isEmpty(locale),
                }"
                @click="handleButtonClicked(locale)"
            >
                {{ locale }}
            </button>
        </template>
    </div>
</template>

<script>
    export default {
        props: {
            locales: {
                type: Array,
                required: true,
            },
            currentLocale: {
                type: String,
                required: true,
            },
            fieldValue: [String, Number, Boolean, Object, Array],
            isLocaleObject: Boolean,
        },
        methods: {
            isActive(locale) {
                return this.currentLocale === locale;
            },
            isEmpty(locale) {
                const value = this.isLocaleObject ? (this.fieldValue || {})[locale] : this.fieldValue;
                return Array.isArray(value) ? !value.length : !value;
            },
            handleButtonClicked(locale) {
                this.$emit('change', locale);
            },
        }
    }
</script>
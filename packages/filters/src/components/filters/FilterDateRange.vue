<template>
    <div class="SharpFilterDateRange" :class="classes">
        <FilterControl :opened="opened" :label="label" :no-caret="noCaret" @click="handleClicked">
            <DateRange
                class="SharpFilterDateRange__field"
                :value="value"
                :display-format="displayFormat"
                :monday-first="mondayFirst"
                :clearable="!required"
                @input="handleInput"
                @focus="handlePickerFocused"
                @blur="handlePickerBlur"
                ref="range"
            />
        </FilterControl>
    </div>
</template>

<script>
    import { DateRange } from 'sharp-form';
    import FilterControl from '../FilterControl';

    export default {
        name: 'SharpFilterDateRange',

        components: {
            DateRange,
            FilterControl,
        },

        props: {
            value: {
                required: true,
            },
            required: Boolean,
            displayFormat: String,
            mondayFirst: Boolean,
            label: String,
        },

        data() {
            return {
                opened: false,
            }
        },

        computed: {
            empty() {
                return !this.value;
            },
            noCaret() {
                return !!this.value && !this.required;
            },
            classes() {
                return {
                    'SharpFilterDateRange--empty': this.empty,
                }
            },
        },

        methods: {
            handleClicked() {
                this.$refs.range.$refs.picker.focus();
            },
            handleInput(range) {
                this.$emit('input', range);
            },
            handlePickerFocused() {
                this.opened = true;
            },
            handlePickerBlur() {
                this.opened = false;
            },
        }
    }
</script>
<template>
    <span class="dropdown control">
        <slot></slot>
        <a
            role="button"
            ref="trigger"
            class="trigger"
            @click="isActive = !isActive">
            <slot name="trigger"></slot>
        </a>

        <transition-group
            appear
            appear-active-class="fadeIn"
            enter-active-class="fadeIn"
            leave-active-class="fadeOut">

            <div
                key="bg"
                class="background is-hidden-desktop"
                v-show="isActive">
            </div>

            <span
                key="dropdown"
                class="box"
                :class="['is-dropdown', {
                    'is-opened-top': !isListInViewportVertically,
                    'is-opened-left': !isListInViewportHorizontally,
                    'is-narrow': narrowed
                }]"
                v-show="isActive"
                ref="dropdown">
                <ul>
                    <template v-for="option in options">
                        <li v-if="option.subheader"
                            class="option"
                            :class="{ 'is-subheader': option.subheader }">
                            <b-icon
                                v-if="option.icon"
                                :icon="option.icon"
                                :pack="option.iconPack">
                            </b-icon>
                            <span v-html="option.label"></span>
                        </li>
                        <li v-else
                            class="option"
                            :class="{
                                'is-selected': option === selected,
                                'is-separator': option.separator,
                                'is-disabled': option.disabled,
                                'is-subheader': option.subheader
                            }"
                            @click="selected = option.value">
                            <b-icon
                                v-if="option.icon"
                                :icon="option.icon"
                                :pack="option.iconPack">
                            </b-icon>
                            <span v-html="option.label"></span>
                        </li>
                    </template>
                </ul>
            </span>

        </transition-group>
    </span>
</template>

<script>
    import SelectMixin from '../../utils/SelectMixin.js'
    import Icon from '../icon'

    export default {
        name: 'bDropdown',
        mixins: [SelectMixin],
        components: {
            [Icon.name]: Icon
        },
        props: {
            narrowed: Boolean
        },
        data() {
            return {
                isDropdown: true // Used internally by SelectMixin
            }
        }
    }
</script>

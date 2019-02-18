<template>
    <renderless-laravel-vue-pagination :data="data" :limit="limit" :show-disabled="showDisabled"
                                       v-on:pagination-change-page="onPaginationChangePage">
        <nav class="pagination" v-if="computed.total > computed.perPage"
             slot-scope="{ data, limit, computed, prevButtonEvents, nextButtonEvents, pageButtonEvents }">
            <div class="column">
                <ul class="pages">
                    <!--<li class="" :class="{'disabled': !computed.prevPageUrl}" v-if="computed.prevPageUrl || showDisabled">
                        <a class="" href="#" aria-label="Previous" :tabindex="!computed.prevPageUrl && -1" v-on="prevButtonEvents">
                            <slot name="prev-nav">
                                <span aria-hidden="true">&laquo;</span>
                                <span class="sr-only">Previous</span>
                            </slot>
                        </a>
                    </li>-->
                    <li v-for="(page, key) in computed.pageRange" :key="key"
                        :class="{ 'active': page == computed.currentPage }">
                        <a href="#" v-on="pageButtonEvents(page)">{{ page }}</a>
                    </li>
                </ul>
            </div>
            <div class="column text-right hidden-xs-down">
                <!--<li :class="{'disabled': !computed.nextPageUrl}" v-if="computed.nextPageUrl || showDisabled">-->
                <!--</li>-->
                <a class="btn btn-outline-secondary btn-sm" href="#" :aria-label="lang('fe.next')"
                   :tabindex="!computed.nextPageUrl && -1" v-on="nextButtonEvents">{{ lang('fe.next') }}&nbsp;
                    <slot name="next-nav">
                        <i class="icon-chevron-right"></i>
                    </slot>
                </a>
            </div>
        </nav>
    </renderless-laravel-vue-pagination>
</template>

<script>
    import RenderlessLaravelVuePagination from './RenderlessLaravelVuePagination.vue';

    export default {
        props: {
            data: {
                type: Object,
                default: () => {
                }
            },
            limit: {
                type: Number,
                default: 0
            },
            showDisabled: {
                type: Boolean,
                default: false
            }
        },

        methods: {
            onPaginationChangePage(page) {
                this.$emit('pagination-change-page', page);
            }
        },

        components: {
            RenderlessLaravelVuePagination
        }
    }
</script>

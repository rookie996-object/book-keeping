<template>
    <div class="tags">
        <ul class="current">
            <li v-for="tag in tagList" :key="tag.id"
                :class="{selected: selectedTags.indexOf(tag)>=0}"
                @click="toggle(tag)">{{tag.name}}</li>
        </ul>
        <div class="new">
            <Icon name="tag"></Icon>
            <button @click="createTag">新增标签</button>
        </div>
    </div>
</template>

<script lang="ts">
    // import Vue from 'vue';
    import {Component} from 'vue-property-decorator';
    import {mixins} from 'vue-class-component';
    import TagHelper from '@/mixins/TagHelper';

    @Component
    export default class Tags extends mixins(TagHelper){
        selectedTags: string[] = [];
        get tagList() {
            return this.$store.state.tagList;
        }

        toggle(tag: string) {
            const index = this.selectedTags.indexOf(tag)
            if(index >= 0) {
                this.selectedTags.splice(index, 1)
            }else {
                this.selectedTags.push(tag);
            }
            this.$emit('update:value', this.selectedTags)
        }
        created() {
            this.$store.commit('fetchTags');
        }
    }
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";
.tags {
    background: white;
    padding: 16px;
    display: flex;
    flex-grow: 1;
    flex-direction: column;
    justify-content: space-between;
    > .current {
        display: flex;
        flex-wrap: wrap;
        > li {
            height: 36px;
            line-height: 36px;
            border-radius: (36px/2);
            padding: 0 16px;
            margin-right: 12px;
            margin-top: 4px;
            box-shadow: inset 5em 1em 0.4;
            background: #ccccff;
            color: white;
            &.selected {
                background: darken(#ccccff, 15%);
            }
        }  
    }
    > .new {
        padding-top: 16px;
        button {
            background: transparent;
            border: none;
            border-bottom: 1px solid;
            color: #999;
            padding: 0 4px;
        }
    }
}
</style>
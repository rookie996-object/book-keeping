<template>
    <nav>
        <router-link to="/labels" class="item" active-class="selected">
            <Icon name="label"></Icon>
            标签
        </router-link>
        <router-link to="/money" class="item" active-class="selected">
            <Icon name="money"></Icon>
            记账
        </router-link>
        <router-link to="/statistics" class="item" active-class="selected">
            <Icon name="statistics"></Icon>
            统计
        </router-link>
    </nav>
</template>

<script lang="ts">

    const importAll = (requireContext: __WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext)
    try {
        importAll(require.context('../assets/icons', true, /\.svg$/))
    } catch (error) {
        console.log(error);
    }

    export default {
        name: 'Nav'
    }
</script>

<style lang="scss" scoped>
    nav{
      display: flex;
      box-shadow: 0 0 3px rgba(0, 0, 0, 0.5);
      flex-direction: row;
      background: #99ccff;
      > .item {
        width: 33.333333%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        font-size: 12px;
        .icon {
          width: 32px;
          height: 42px;
        }
      }
      > .item.selected {
          color: #ffffff;
      }
    }
    
</style>
<template>
    <div class="select">
      <span class="select-value" @click.stop='showOptions'><strong class="value text-overflow" :title="value" :data-value='selectedRealValue'>{{value}}</strong><i class="fa fa-sort-down"></i></span>
      <ul class="select-options" v-show='optionsShow' @click="select($event)">
        <slot></slot>
      </ul>
    </div>
</template>

<script>
/*
  * author: litingting
  * data: 2017.04.27
  * des: 这是一个公用的select下拉框组件，采用vue开发
  * options： 需要从父组件传递一个值，默认选择项：seletedValue；
  *           列表项通过slot在父组件中处理；
  *           选取某一项时会触发select事件，然后$emit到父组件，可以在父组件监听该事件进行相应处理；
  * structure: <bio-select ref='select' :selectedValue='selectedText' @select='select'>
            <li v-for='option in options' :data-value='option.attrTypeEn'>{{option.attrTypeZh}}</li>
          </bio-select>
  *
 */
/* eslint-disable no-undef */

  export default {
    props: {
      options: Array,
      selectedValue: String,
      selectedRealValue: String
    },
    data () {
      return {
        value: this.selectedValue,
        optionsShow: false
      }
    },
    mounted () {
      $('body').off('click.select').on('click.select', function (e) {
        this.$parent.$children.forEach((item, index) => {
          if (item.optionsShow !== undefined) {
            item.optionsShow = false;
          }
        });
      }.bind(this));
    },
    methods: {
      showOptions () {
        var temp = this.optionsShow;
        this.$parent.$children.forEach((item, index) => {
          if (item.optionsShow !== undefined) {
            item.optionsShow = false;
          }
        });
        this.optionsShow = !temp;
      },
      select (e) {
        this.value = $(e.target).text();
        this.optionsShow = false;
        this.$emit('select', $(e.target).data());
      }
    }
  }
</script>
<style lang="less" scoped>
  @bs : 1px solid #e7e7e7;
  .select{
    @sw : 150px;
    display: inline-block;
    position: relative;
    vertical-align: middle;
    .select-value{
      border: @bs;
      display: inline-block;
      width: @sw;
      line-height: 26px;
      strong{
        display: inline-block;
        padding-left: 5px;
        width: @sw - 30;
      }
      i{
        border-left: @bs;
        display: inline-block;
        line-height: 26px;
        text-align: center;
        width: 28px;
      }
    }
    .select-options{
      background: #fff;
      border: @bs;
      border-top: none;
      padding: 0;
      position: absolute;
      width: @sw - 28;
      max-height: 100px;
      overflow: auto;
      z-index: 2;
      li{padding: 5px 5px; cursor: pointer; width: @sw - 28;}
      li:hover{
        background: #ccc;
      }
    }
  }
</style>

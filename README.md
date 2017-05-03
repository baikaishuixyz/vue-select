## vue-select

This is a vue select component.
---

## props

1. selectedValue   默认选中的值，用于页面展示
2. selectedRealValue 默认选中的值，用于传递给后端

## usage

  	<bio-select :selectedValue='selectedText' :selectedRealValue='selectedRealValue'  @select='select'>
    	<li v-for='option in options' :data-value='option.attrTypeEn'>{{option.attrTypeZh}}</li>
  	</bio-select>`



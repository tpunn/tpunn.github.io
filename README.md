# tpunn.github.io

**Circle animation component**
(Requires Vue.js)

"Option" generates random class to assign from array.
Props are different styles: size, position, color.
Template binds class and style using the props and option value.

```
Vue.component('shape-circle', {
  data() {
     return {
        option: ["bounce","float1","float2","bounce"][Math.floor(Math.random()*4)]
     }
  },
  props: ['radius','ypos','xpos','bg'],
  template: `<div :class="option" :style="{animationDelay:Math.floor(Math.random()*10)/2+'s',width:radius*2+'px',height:radius*2+'px',top:ypos-radius/2+'px',left:xpos-radius/2+'px',backgroundColor:bg}"></div>`
})
```

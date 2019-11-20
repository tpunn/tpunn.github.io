# tpunn.github.io

**Typewriter method**

- Initialize Vue Instance. Important data: finishing text, empty string, speed, character index, and if pipe should display at end (boolean).
- Computed created created to return a pipe concatenated to the empty string. Uses ternary statement for quick condition. Unfortunately, can't use arrow functions inside Vue instance, but composition API in Vue 3 can change that.
- The only method we need is the initialization of the typewriter. The method uses recursion to post a new character to the empty string each time. Additionally, a mounted event is written too alternate the pipe boolean every 500 milliseconds.
- WARNING: Use v-html to interpolate the name() computed to the &lt;h1&gt; because it uses html in the string, not plain text.

```
let app = new Vue({ 
el: '#app', 
data: {
txt: 'Tony Punnacherry',
txt2: '',
speed: 150,
i: 0,
pipe: true,
},
computed: {
name() {return this.txt2.concat(this.pipe ? "<span class='pipe'>|</span>" : "")}
},
methods: {
typeWriter() {
  if (this.i < this.txt.length) {
    this.txt2 += this.txt.charAt(this.i)
    this.i++
    setTimeout(this.typeWriter, this.txt.charAt(this.i)==" " ? 300 : this.speed)
  } else {
    this.i = 0
  }
}
},
mounted() {
this.typeWriter()
let t = this;
setInterval(()=>{
t.pipe = !t.pipe
},500);
}
})
```

**Circle animation component**

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

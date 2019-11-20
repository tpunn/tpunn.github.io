# tpunn.github.io

**Typewriter method**

- Initialize Vue Instance. Important data: finishing text, empty string, speed, character index, and if pipe should display at end (boolean).
- Computed created created to return a pipe concatenated to the empty string. Uses ternary expression for simple conditioning. Unfortunately, can't use arrow functions inside Vue instance, but composition API in Vue 3 can change that.
- The only method we need is the initialization of the typewriter. The method uses recursion to post a new character to the empty string each time. Additionally, a mounted event is written too alternate the pipe boolean every 500 milliseconds.
- WARNING: Use v-html to interpolate the name() computed to the `&lt;h1&gt;` because it uses HTML in the string.

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

**CSS Tips**

- `background-attachment: fixed` is super useful for creating parallax experiences. If you want a slow scroll, using an onscroll event is a better idea. I might update this in the future.
- Working with `@keyframes`... CSS animations are easy and great. It doesn't have the full power that JavaScript embraces, but for simple animations, it is much better than scripting it. CSS animations come with many different properties, allowing you to create bezier curves rather than linear animations. It also comes with infinite looping, and a DOM API. All you need to do is set CSS state in a percentage progress. You can search it up online.
- `:before and :after` are one of the most useful ways to add custom elements to your HTML. Most inexperienced people jump to JavaScript for adding reusable elements (such as an icon, or label) into a certain class. Using the CSS way is much faster, and allows you to easily work with CSS as well. If you don't need any JavaScript and just static text or CSS-made shapes, you can use before and after. You can search it up online.

I'll put links to references (or write my own) to these later.

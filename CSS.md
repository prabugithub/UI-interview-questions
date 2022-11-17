# CSS interview/reference question and answers
1. [Responsive design](https://github.com/prabugithub/angular-interview-questions/edit/main/CSS.md#responsive-design)

## Responsive design

### Image responsive

* We could use picture tag
* If use picture tag we could bind selective image for each layout so that it gives good resolution to the user
* In the below code picture will load based on the media attribute value.
```html
<picture>
  <source media="(max-width:1000px)" srcset="picture-lg.png">
  <source media="(max-width:600px)" srcset="picture-mid.png">
  <source media="(max-width:400px)" srcset="picture-sm.png">
  <img src="picture.png" alt="picture"">
</picture>
```
### Flex & flex wrap
* Better decouple the layout we need to use flex instead split into grid design. So that we can modify layout easyly using the css and help of media query.
[flex box tricks](https://css-tricks.com/responsive-layouts-fewer-media-queries/)
[demo](https://codepen.io/t_afif/pen/wvgVVPN)

[css simple play demo](https://www.w3schools.com/cssref/playdemo.php?filename=playcss_flex-direction)

html,
```html
<div class="container">
  <div></div>
  <div></div>
  <div></div>
  <div></div>
  <div></div>
</div>
```
CSS,
```css
.container {
  display:flex;
  flex-wrap:wrap; /* this */
  gap:10px;
}
.container > div {
  height:100px;
  flex:400px; /* and this */
  background:red;
}
```

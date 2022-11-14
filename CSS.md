# CSS interview/reference question and answers

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

Topic: Handlebars
Date: 1/31/18
***
Link: http://handlebarsjs.com/
Slides: http://devleague.slides.com/devleague/handlebars

## Partials
```javascript
{{> header}}
```

## Helpers (iterators)

In this example, the comments are being iterated through to generate the appropriate amount of HTML.
```javascript
//data injected
let commentsCollection = {
  comments: [
    {title: "Hello", text: "This is dog"},
    {title: "I Love Pie", text: "I cannot lie"}}
  ]
}

res.render('comments', commentsCollection)
```
```html
<div class="comments">
  {{#each comments}}
    <div class="comment">
        <h2>{{title}}</h2>
        <p>{{text}}</p>
    </div>
  {{/each}}
</div>
```

## Conditionals

```javascript
//data injected
let data = {
  showContent: true,
  content: "Show me the money!"
}

res.render('home', data)
```

```html
// home template

{{#if showContent}}
  <p>{{content}}</p>
{{else}}
  <p>No Content Available</p>
{{/if}}
```

### вибери всі посилання зі сторінки в вигляді markdown нумерованого списка

```javascript
// Find all anchor tags with rel="bookmark"
var bookmarkLinks = document.querySelectorAll('a[rel="bookmark"]');

// Collect the formatted Markdown links in an array
var markdownLinks = [];
bookmarkLinks.forEach(function(link) {
  var href = link.getAttribute('href');
  var text = link.textContent.replace(/\s+/g, ' ').trim();
  var markdownLink = '[' + text + '](' + href + ')';
  markdownLinks.push(markdownLink);
});

// Convert the array to a numeric Markdown list
var markdownList = markdownLinks.map(function(link, index) {
  return (index + 1) + '. ' + link;
}).join('\n');

// Output the numeric Markdown list
console.log(markdownList);

```


### вибери всі посилання зі сторінки в вигляді markdown todoList
```javascript
// Find all anchor tags with rel="bookmark"
var bookmarkLinks = document.querySelectorAll('a[rel="bookmark"]');

// Collect the formatted Markdown links in an array
var markdownLinks = [];
bookmarkLinks.forEach(function(link) {
  var href = link.getAttribute('href');
  var text = link.textContent.replace(/\s+/g, ' ').trim();
  var markdownLink = '[ ] [' + text + '](' + href + ')';
  markdownLinks.push(markdownLink);
});

// Convert the array to a numeric Markdown list
var markdownList = markdownLinks.map(function(link, index) {
  return '- ' + link;
}).join('\n');

// Output the numeric Markdown list
console.log(markdownList);

```

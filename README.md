# Sheetsee-tables

see: [jlord.github.io/sheetsee.js](http://jlord.github.io/sheetsee.js)
demo: [tables](http://jlord.github.io/sheetsee.js/demos/demo-table.html)

With this module you can create tables of your data that are sortable, searchable and paginate-able.

You'll need a placeholder `<div>` in your html, a `<script>` [mustache](https://mustache.github.io) template and a `<script>` that initiates the table.

## Your HTML Placeholder

This is as simple as an empty `<div>` with an id.

## Your Template

Your template is the mockup of what you'd like your table to look like and what content it should show. The style is up to you! It is a [mustache](https://mustache.github.io) template inside of `<script>` tags.

**The `id` of the template should be the same as the HTML placeholder it corresponds to but with "_template" on the end.**

### Sorting

If you want users to be able to click on headers and sort that column, your template must include table headers with the class `tHeader`.

You can then style `.tHeader` in your CSS to make them look how you want.

## Your Script

You'll want to set your table options and pass them into `Sheetsee.makeTable()`. If you want to add a search/filter, pass your options into `Sheetsee.initiateTableFilter()`

## Methods

Functions for you to use! There are just two :tada:

### `Sheetsee.makeTable(tableOptions)`

You pass in an object containing:

- `data` _array_ your data from Tabletop.js
- `pagination` _number_ how many rows displayed at one time, defaults to all
- `tableDiv` _string_ the `<div>` `id` placeholder in your HTML, includes the hash `#`
- `filterDiv` _string_ the `<div>` `id` containing your `<input>` filter if using search, includes the hash `#`
- `templateID` _string_ the `id` of your `<script>` tag with the template, defaults to assume it's the same as `tableDiv` + `_template`.

```javascript
var tableOptions = {
                    "data": data,
                    "pagination": 10,
                    "tableDiv": "#fullTable",
                    "filterDiv": "#fullTableFilter",
                    "templateID": "fullTable"
                    }
Sheetsee.makeTable(tableOptions)
```

#### Pagination

If you do not put in a number for pagination, by default it will show all of the data at once. With pagination, HTML will be added at the bottom of your table for navigation, which you can style in your CSS:

_HTML_

```HTML
<div id='Pagination' currentPage class='table-pagination'>
  Showing page {{currentPage}} of {{totalPages}}
  <a class='pagination-pre'>Previous</a><a class='pagination-next'>Next</a>
</div>
```

_CSS_

```CSS
#Pagination {}
.pagination-next {}
.pagination-pre {}
.no-pag {}
```

## `Sheetsee.initiateTableFilter(tableOptions)`

If you want to have an input to allow users to search/filter the data in the table, you'll add an input to your HTML. Give it an id and if you want add placeholder text:

```javascript
<input id="tableFilter" type="text" placeholder="filter by.."></input>
```

Then you'll pass your `tableOptions` object into this method:

```javascript
Sheetsee.initiateTableFilter(tableOptions)
```

You should also add a 'clear' button using the `.clear` CSS class.

```HTML
<a href="#" class=".clear">Clear</a>
```

## Example

_HTML_

```HTML
<input id="siteTableFilter" type="text"></input><a href="#" class=".clear">Clear</a>
<div id="siteTable"></div>
```

_Template_

```JavaScript
<script id="tableTemplate" type="text/html">
    <table>
    <tr><th class="tHeader">City</th><th class="tHeader">Place Name</th><th class="tHeader">Year</th><th class="tHeader">Image</th></tr>
      {{#rows}}
        <tr><td>{{city}}</td><td>{{placename}}</td><td>{{year}}</td><td>{{image}}</td></tr>
      {{/rows}}
  </table>
</script>
```

_JavaScript_

```javascript
<script type="text/javascript">
  document.addEventListener('DOMContentLoaded', function() {
    var tableOptions = {
                        "data": data,
                        "pagination": 10,
                        "tableDiv": "#siteTable",
                        "filterDiv": "#siteTableFilter",
                        "templateID": "tableTemplate"
                        }
    Sheetsee.makeTable(tableOptions)
    Sheetsee.initiateTableFilter(tableOptions)
  })
</script>
```

_[View Demo](/demos/demo-table.html)_

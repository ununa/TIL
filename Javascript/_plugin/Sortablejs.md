# Sortablejs

### Simple list example
``` js
new Sortable(example1, {
    animation: 150,
    ghostClass: 'blue-background-class'
});
```

#### Usage
``` html
<ul id="items">
	<li>item 1</li>
	<li>item 2</li>
	<li>item 3</li>
</ul>
```
``` js
var el = document.getElementById('items');
var sortable = Sortable.create(el);
```

#### Options
``` js
var sortable = new Sortable(el, {
    ... options
});
```

### Option: disabled
#### setting
``` js
var _lnbSortable = Sortable.create(lnbSortable, {
        animation: 150,
        sort: true,
        disabled: true, // off
        items: ':not(.is-recomm)',
        filter: '.is-recomm', 
        store: { ... }
});
```

#### on
``` js
_lnbSortable.option('disabled', false);
```

#### off
``` js
_lnbSortable.option('disabled', true);
```






link 1: https://github.com/SortableJS
link 2: https://jsbin.com/sewokud/edit?js,output
link 3: https://github.com/SortableJS/Sortable/issues



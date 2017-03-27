Page Sort and Move
==================

Module extends page API with capability to move/sort at any time.   

## Current situation
If a new page is created in PW it will be appended to its siblings. Until now there is now built-in function to change this. Neither during creation nor later.  
  
**@horsts** module **[Pagetree Add New Childs Reverse](http://modules.processwire.com/modules/page-tree-add-new-childs-reverse/)** provides the option to prepend the new created page to its siblings instead of appending. You can assign this to specific templates and/ or parents via module settings.  

### Retrieving Data  
If you want to retrieve the pages sort value you can use: `$page->sort`; To get the exact position related to its siblings, use: [`$page->index`](https://processwire.com/api/ref/page/index/);  

_Example: if you have 3 siblings with sort values: 0,4 and 7 the page with the sort value 4 is the second sibling and will therefore carry the index 1 (zero-based)_  
  
## Extended Page API with this module


| Name | Return | Summary | 
|:--|:--|:--|
| `$page->sort($newIndex)` | bool/ null | Set a new sort index relative to the page parents. If the value is negative, the new index will be counted back from the total number of siblings. If 0 page will be appended if equal or bigger than number of siblings page will be the last under its siblings.|
| `$page->move($newIndex, $parentID = null)` | bool/ null | Same as before but with capability to change the parent too. |
| `$page->moveFirst($parentID = null)` | bool/ null | Set page as first under its siblings.<br>`$page->sort = 0`<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->moveFirst`</small> |
| `$page->moveLast($parentID = null)` | bool/ null | Set page as last under its siblings.<br>`$page->sort = $page->parent->numChildren()`<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->moveLast`</small>  |

## Callable Functions
 
 ```  
// STATIC  
PageSortMove::execute($pageID, $newIndex = 0, $parentID = null);

// INSTANCE
 $modules->get('PageSortMove')->execute($pageID, $newIndex = 0, $parentID = null);
 
// RETURN  
// NULL if nothing to change
// TRUE in case of success
// FALSE in case of failure
 ```

## Coming soon 
Change sort order based on page field or property. Expecting string parameter like 'id', 'modified' or 'mypagefield.id'. Optionally reverse order.
```
$page->sortSiblings($sortSelectorValue, $rev = 0)
$page->sortChildren($sortSelectorValue, $rev = 0)
```

## License
[GNU-GPLv3](http://www.gnu.org/licenses/gpl-3.0.html)

## Author
kixe (Christoph Thelen)

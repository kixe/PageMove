Page Sort and Move
==================

Module extends page API with capability to move/sort.   

## EXTENDED PAGE API


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

## License
[GNU-GPLv3](http://www.gnu.org/licenses/gpl-3.0.html)

## Author
kixe (Christoph Thelen)

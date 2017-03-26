Page Sort and Move
==================

Module extends page API with capability to move/sort page   

## EXTENDED PAGE API


| Name | Return | Summary | 
|:--|:--|:--|
| `$page->sort($newIndex)` | bool | Set a new sort index relative to the page parents. If the value is negative, the new index will be counted back from the total number of siblings.|
| `$page->move($newIndex, $parentID = null)` | bool | Same as before but with capability to change the parent too. |
| `$page->first($parentID = null)` | bool | Set page as first under its siblings.<br>`$page->sort == 0`<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->first`</small> |
| `$page->last($parentID = null)` | bool | Set page as last under its siblings.<br>`$page->sort == $page->parent->numChildren()`<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->last`</small>  |

## Callable Functions
 
 ```  
// STATIC  
PageSortMove::execute($pageID, $newIndex = 0, $parentID = null);

// INSTANCE
 $modules->get('PageSortMove')->execute($pageID, $newIndex = 0, $parentID = null);
 ```

## License
[GNU-GPLv3](http://www.gnu.org/licenses/gpl-3.0.html)

## Author
kixe (Christoph Thelen)

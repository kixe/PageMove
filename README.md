Page Move and Resort
====================

Module extends page API with capability to move/ resort a page related to parent and siblings.  

## Current situation
  + Using `$page->sort` as a **setter** will not affect siblings. After using this call another sibling may have the same sort value.
  + `page->index` doesn't work as a setter. `page->index` take in account only published, unhidden pages and therefore return unexpected results:  

	_In the following example we get 3 pages with the same index (3)_
	
	```
	$siblings = $page->siblings('include=all');
	var_dump($siblings->each('index')); 
	
	// return  
	array(6) {
	  [0]=> int(3) // id=2, sort=1, admin
	  [1]=> int(0) // id=1033, sort=6
	  [2]=> int(1) // id=1036, sort=10
	  [3]=> int(3) // id=27, sort=14, (404) hidden
	  [4]=> int(3) // id=7, sort=17, (trash) hidden
	  [5]=> int(2) // id=1024, sort=100
	}  
	```  





  + The built-in functions `Pages::sort()` is limited, since it will change the absolute sort value and not the index (position) of a page related to its siblings. 
  
**@horsts** module **[Pagetree Add New Childs Reverse](http://modules.processwire.com/modules/page-tree-add-new-childs-reverse/)** provides the option to **prepend** the new created page to its siblings instead of **appending**. You can assign this to specific templates and/ or parents via module settings. Thanks @horst.
  
## Extended Page API with this module


| Name | Return | Summary | 
|:--|:--|:--|
| `$page->move($parent, $newIndex = null, $selector = 'all')` | bool/ null | Set a new index relative to the siblings under the future page parent. If the value is negative, the new index will be counted back from the total number of siblings. If 0 page will be appended if equal or bigger than number of siblings page will be the last under its siblings.|
| `$page->setIndex($newIndex, $selector = 'all')` | bool/ null | Set the pages index position related to its siblings|
| `$page->getIndex($selector = '')` | int/ bool | Return the index related to all siblings included via selector. Return false if the page is not an element of the selected siblings (if limited by selector)|
| `$page->moveFirst($parentID = null)` | bool/ null | Set page as first (absolute) under its siblings.<br>`$page->sort = 0`, no duplicates.<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->moveFirst`</small> |
| `$page->moveLast($parentID = null)` | bool/ null | Set page as last (absolute) under its siblings.<br>`$page == $page->siblings('include=all')->last();`<br>Optionally change the parent by adding the corresponding ID as a single parameter.<br><small>Can also be used as property:<br>`$page->moveLast`</small>  |
| `$page->moveForward($steps = 1, $selector = 'all')` | bool/ null  |  move` $steps` steps forward  related to siblings defined in selector | 
| `$page->moveBackwards($steps = 1, $selector = 'all')` | bool/ null  |   move` $steps` steps backwards related to siblings defined in selector  |  
| `$pages->move($page, $parent = null, $newIndex = 0, $selector = 'all')` | bool/ null | move to any new parent and any index related to siblings defined in selector |  
| `$pages->resortChildren($page, $selectorValue)` | bool/ null | resort children under specified parent based on selector value `(sort=$selectorValue)` |  
 

**$newIndex**  
should be an int value. If negative the new index will be found counting back from the end.

**$selector**  
can be either int value `(status=$selector)` or one of the strings: 'all', 'hidden', 'unpublished', 'trash'
`(include=$selector)`
If the specified page is not part of the family nothing will be changed.


## Callable Functions
 
 ```  
// STATIC  
PageMove::execute($page, $parent = null, $newIndex = 0, $selector = 'all');

// INSTANCE
$modules->get('PageMove')->execute($page, $parent = null, $newIndex = 0, $selector = 'all'); 
 
// RETURN
// NULL if nothing has been changed  
// INT if the parent has been changed but the index not
// TRUE in case of success (index changed, parent maybe)
// FALSE in case of failure

PageMove::getIndex($page, $selector = '');  
// RETURN 
// INT index
// FALSE $page itself is excluded from its siblings via selector
 ```

## License
[GNU-GPLv3](http://www.gnu.org/licenses/gpl-3.0.html)

## Author
kixe (Christoph Thelen)

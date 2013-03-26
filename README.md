openlss/lib-router
==========

Router for handling web calls, allows dynamic registration at runtime

Usage
----
```php
use \LSS\Router;

Router::init();
Router::_get()->setRoot(ROOT);
Router::_get()->setDefault('/ctl/home.php');
Router::_get()->register('client','list'=>'/ctl/client_list.php');
$dest = Router::_get()->route(get('act'),get('do'),get('fire'));
require($dest);
```

Reference
----

### (void) Router::init()
Calls the construct and starts the singleton

### (object) Router::_get()
Returns the current instance

### (string) Router::setDefault($dest)
Sets the default file to route too. Relative to root.

### (string) Router::setRoot($root)
Set the root folder that all route calls are relative to.

### (object) Router::register($act,$do=array())
  * $act		The first routing argument
  * $do			An array of secondary routing arguments
   * Do may also contain arrays of "fire" routing calls
The router is tertiary

A more in depth example
```php
Router::_get()->register('client',array(
	 'list'		=>	'/ctl/client_list.php'
	,'edit'		=>	'/ctl/client_edit.php'
	,'create'	=>	'/ctl/client_create.php'
	,'manage'	=>	array( //this is a tiertiary segment
		'contacts'		=>	'/ctl/client_manage_contacts.php'i
		 //set the default when the third segment is missing
		Router::DEF		=>	'/ctl/client_manage.php'	
	)
	//set the default when the second segment is missing
	,Router::DEF	=>	'/ctl/client_list.php'
));
```

### (string) Router::route($act=null,$do=null,$fire=nul)
  * $act		The first routing segment usually a get variable
  * $do			The second routing segement usually a get variable
  * $fire		The thrist routing segment
Returns the controller to route to which should then be sent to require()


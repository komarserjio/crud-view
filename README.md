crud-view
=========

(Incubator project) Automated admin backend based on your Crud configuration

This project is in very very early stage of development, do not use it production unless you want to get down and dirty on the code :)

Usage
=====

1) Make sure to follow the normal CRUD install settings.

2) Install this plugin using `composer require --prefer-dist friendsofcake/crud-view:~dev-master`.

2) Add `Plugin::load('CrudView');` and  `Plugin::load('BootstrapUI');` in your `app/config/bootstrap.php`.

3) Change `AppController::$viewClass` to `CrudView\View\CrudView`.

4) Load the `CrudView.View`, `Crud.RelatedModels` and `Crud.Redirect` listeners.

5) Hopefully going to `/<your controller with crud enabled/` should just work.

Example controller
==================

```php
<?php
namespace App\Controller;

use Cake\Controller\Controller;
use Crud\Controller\ControllerTrait;

class AppController extends Controller
{
    use ControllerTrait;

    public function initialize()
    {
        parent::initialize();

        $this->loadComponent('RequestHandler');
        $this->loadComponent('Flash');
        
        $this->viewClass = 'CrudView\View\CrudView';
        $this->loadComponent('Crud.Crud', [
            'actions' => [
                'Crud.Index',
                'Crud.Add',
                'Crud.Edit',
                'Crud.View',
                'Crud.Delete',
            ],
            'listeners' => [
                'CrudView.View',
                'Crud.RelatedModels',
                'Crud.Redirect',
            ],
        ]);
    }
}
```

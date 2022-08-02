# Laravel Repositories generator
 

Laravel Repositories generator is a package for Laravel 7, 8 and 9 which is used to generate reposiotries from eloquent models.

## Installation

Run the following command from you terminal:


 ```bash
 composer require "mveabraham/repository-generator"
 ```

## Usage

First, generate your repositories class from eloquent models in Models folder.
 ```bash
 php artisan make:repositories
 ```
And finally, use the repository in the controller:

```php
<?php namespace App\Http\Controllers;

use App\Repositories\PostRepository;

class PostController extends Controller {

    private $postRepository;
    
    public function __construct(PostRepository $postRepository)
    {
        $this->postRepository = $postRepository;
    }

    public function index() {
        return response()->json($this->postRepository->getAll());
    }
}
```
## Available Methods

The following methods are available:

##### MveAbraham\RepositoryGenerator\RepositoryInterface

```php
    public function exists(string $key, $value, $withTrashed = false)

    public function getByAttribute(string $attr_name, $attr_value, $relations = [], $withTrashed = false, $selects = [])

    public function getPaginate(int $n, $relations = [], $withTrashed = false, $selects = []);

    public function store(Array $inputs)

    public function getById($id, $relations = [], $withTrashed = false, $selects = [])

    public function search($key, $value, $relations = [], $withTrashed = false, $selects = [])

    public function getAll($relations = [], $withTrashed = false, $selects = [])

    public function countAll($withTrashed = false)

    public function getAllSelectable($key)

    public function update($id, Array $inputs)

    public function destroy($id)

    public function destroyAll()

    public function forceDelete($id)

    public function restore($id)
```

### Example usage

Create a new post in repository:

```php
$post = $this->postRepository->store($request->all());
```
Update existing post:

```php
$post = $this->postRepository->update($post_id, $request->all());
```

Delete post:
```php
$post = $this->postRepository->destroy($id);
```

Get post by post_id:
```php
$post = $this->postRepository->getById($id);
```

you can also chose what relations to eager load:
```php
$post = $this->postRepository->getById($id, ['comments']);
```

## Credits

This package is inspired by [this](https://github.com/bosnadev/repository) great package by @bosnadev.

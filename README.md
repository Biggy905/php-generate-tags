# PHP Generate Tags
___
HTML tags source code generation based on configuration OOP.
### Installation
```
composer require biggy905/php-generate-tags
```
### Basic usage
___
```php
use GenerateTags\Tag;
use GenerateTags\TagRenderable;

$tag = new Tag('div');
$render = (new TagRenderable())
    ->addTag($tag)
    ->addContent('Hello world!')
    ->render();

echo $render;
/*
Output:
<div>Hello world!</div>
 */

$tag = new Tag('div');
$render = (new TagRenderable())
    ->addTag($tag)
    ->addContent('Best PHP')
    ->addAttributes(
        [   
            'class' => 'container',
            'data-custom' => 'data',
        ]
    )
    ->render();

echo $render;
/*
Output:
<div class="container" data-custom="data">Best PHP</div>
*/
```
### Other usage
___
```php
$tagUl = new Tag('ul');
$tagLi = new Tag('li');
$tagA = new Tag('a');

$render = (new TagRenderable())
    ->addTag($tagUl)
    ->addAttributes(
        [   
            'class' => 'page_list',
            'data-status' => 'show',
        ]
    )
    ->addContent(
        (new TagRenderable())
            ->addTag($tagLi)
            ->addAttributes(
                [
                    'class' => 'page_item',            
                ]           
            )
            ->addContent(
                 (new TagRenderable())
                    ->addTag($tagA)
                    ->addAttributes(
                        [
                            'href' => 'first.html',
                            'target' => '_blank',                
                        ]           
                     )
                     ->content('First Page')
                     ->render()
            )
            ->render(),
        (new TagRenderable())
            ->addTag($tagLi)
            ->addAttributes(
                [
                    'class' => 'page_item',           
                ]           
            )
            ->addContent(
                 (new TagRenderable())
                    ->addTag($tagA)
                    ->addAttributes(
                        [
                            'href' => 'second.html',               
                        ]           
                    )
                    ->addContent('Second Page')
                    ->render()
            )
            ->render(),
    )

    ->render();

echo $render;

/*
Output:
<ul class="page_list" data-status="show">
    <li class="page_item">
        <a href="first.html" target="_blank">First Page</a>
    </li>
    <li class="page_item">
        <a href="second.html">Second Page</a>
    </li>
</ul>
*/
```

### License
___
PHP Generate Tags is open-sourced software licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php).
Copyright © 2024.
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
### Another usage
___
```php
use GenerateTags\Tag;
use GenerateTags\TagRenderable;

$tagRenderable = new TagRenderable();

$tagDiv = new Tag('div');
$tagSpan = new Tag('span');
$tagH3 = new Tag('h3');
$tapP = new Tag('p');

$items = [
    [
        'product' => 'Product 1',
        'price' => 3600,    
    ],
    [
        'product' => 'Product 2',
        'price' => 4200,    
    ],
    [
        'product' => 'Product 3',
        'price' => 1200,    
    ],        
];

$tagRenderableItems = [];
foreach ($items as $item) {
    $tagRenderableItems[] = $tagRenderable
        ->clear()
        ->addTag($tagDiv)
        ->addAttributes(
            [
                'class' => 'col-3',            
            ]       
        )
        ->addContent(
            $tagRenderable
                ->clear()
                ->addTag($tagH3)
                ->addAttributes(
                    [
                        'class' => 'text-center'
                    ],                
                )
                ->addContent($item['product'])
                ->render(),
            $tagRenderable
                ->clear()
                ->addTag($tagP)
                ->addContent($item['price'])
                ->render(),   
        )
        ->render();
}

$render = $tagRenderable
    ->clear()
    ->addTag($tagDiv)
    ->addAttributes(
        [
            'class' => 'container',
        ]
    )
    ->addContent(
        $tagRenderable
            ->addTag($tagDiv)
            ->addAttributes(
                [
                    'class' => 'row',
                ]       
            )
            ->addContent(
                $tagRenderableItems
            )
            ->render();
    );
    
echo $render;
/*
output:
<div class="container">
    <div class="row">
        <div class="col-3">
            <h3 class="text-center">
                Product 1
            </h3>
            <p>
                3600
            </p>
        </div>
        <div class="col-3">
            <h3 class="text-center">
                Product 2
            </h3>
            <p>
                4200
            </p>
        </div>
        <div class="col-3">
            <h3 class="text-center">
                Product 3
            </h3>
            <p>
                1200
            </p>
        </div>
    </div>
</div>
*/

```
### License
___
PHP Generate Tags is open-sourced software licensed under the [MIT license](https://mit-license.org/license.txt).
Copyright © 2024.
# yii2-grid-view-state
Save filters from GridView to session, keep the filter state between pages.

## Features
1. Very flexible. Separate setting and getting.
2. Setting via behavior.
3. Determines the uniqueness by the action route and a customizable ID.

## Installation
Add this repository to your `composer.json`

```json
{
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/thrieu/yii2-grid-view-state.git"
        }
    ]
}
```

Then run

```
composer require --prefer-dist thrieu/yii2-grid-view-state "dev-master"
```

## Usage
### Step 1
Extend GridView class, simply implement FilterStateInterface and FilterStateTrait.
```php
namespace \app\widgets;

use thrieu\grid\FilterStateInterface;
use thrieu\grid\FilterStateTrait;

class GridView extends \yii\grid\GridView implements FilterStateInterface {
    use FilterStateTrait;
}
```
### Step 2
Attach the filter behavior to your GridView widget.
```php
GridView::widget([
...
    'as filterBehavior' => \thrieu\grid\FilterStateBehavior::className(),
...
]);
```
### Step 3
Get the params which merging the GridView state params with GET query params and set it to the filter model and the DataProvider.
```php
// Filter model
$model->load(GridView::getMergedFilterStateParams());
// DataProvider
$dataProvider = new ActiveDataProvider([
    'query' => $query,
    'pagination' => [
        'params' => GridView::getMergedFilterStateParams(),
    ],
    'sort' => [
        'attributes' => $attributeOrders,
        'params' => GridView::getMergedFilterStateParams(),
    ],
]);
```

## Roadmap
The functionality of clearing state would be added in the nearly future.

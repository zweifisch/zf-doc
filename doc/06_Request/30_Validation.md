
describe input schema using [json-scheme](http://json-schema.org/), schemas should be located in folder `schemas` by default

`schemas/product.json`

```javascript
{
	"title": "creating a product",
	"type": "object",
	"properties": {
		"name": {
			"type": "string",
			"maxLength": 32,
			"minLength": 2,
		}
		"desc": {
			"type: "string",
			"maxLength": 2046,
		}
		"price": {
			"type": "number",
			"multipleOf": 0.01
		}
	}
	"required": ["name", "desc", "price"]
}
```

if the input faild the validation, errors are pushed to `$this->errors`

```php
/**
 * @schema product.json
 */
return function() {
	if ($this->errors) {
		$this->response->status = 400;
		return $this->errors;
	} else {
		return $this->mongo->products->insert($this->body);
	}
};
```


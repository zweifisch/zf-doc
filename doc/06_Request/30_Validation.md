
describe input schema using [json-scheme](http://json-schema.org/), schemas should be located in folder schemas by default

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

if the input validates against the schema, `$this->body` will be populated as a `stdObject` or array; otherwise, errors are pushed to `$this->errors` and `$this->body` will be set to null

```php
/**
 * @body product.json
 */
return function() {
	if ($this->body) {
		return $this->mongo->products->insert($this->body);
	} else {
		return $this->errors;
	}
};
```


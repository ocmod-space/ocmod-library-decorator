# Library Decorator

## Description
A library decorator module for OpenCart that extends `Cart\Cart` and `Cart\Tax` classes with support for pre- and post-method events. It enables advanced modifications via the event system without changing core library files.

Compatible with OpenCart 3.x/4.x (PHP 7.x and above).

## Features
- **Event Triggers**: The module allows you to define custom events that can be triggered before and after the execution of core library methods. This enables you to execute custom code at specific points in the method execution process.
- **No Core Modifications**: The module does not require any modifications to the core OpenCart code, ensuring that your customizations are safe from being overwritten during updates.
- **Compatibility**: The module is compatible with OpenCart 3.x and 4.x, ensuring that it works seamlessly with the latest versions of the platform.

## Usage
To hook into methods of decorated library classes like `Cart\Cart` or `Cart\Tax`, you can register custom events in your module's install() method using the OpenCart Event system.

In the example below, the event is triggered after the `getProducts` method of the `Cart\Cart` class is executed.

```php
$this->load->model('setting/event');

$event_code = 'your_module_cart_getProducts';
$trigger = 'library/cart/cart/getProducts/after';
$action = 'extension/your_module/event/cart/getProductsAfter';

// OC 3.x
$this->model_setting_event->addEvent($event_code, $trigger, $action);

// OC 4.x
$this->model_setting_event->addEvent([$event_code, $trigger, $action]);
```

The `getProductsAfter` method in your module will be called with the following parameters:
- `$route`: The route of the method being executed (e.g., `library/cart/cart/getProducts`).
- `$args`: An array of arguments passed to the method.
- `$output`: The output of the method being executed.
You can then modify the `$output` variable or perform any other actions you need.

```php
public function getProductsAfter(&$route, &$args, &$output) {
    // Your custom code here
    // $output contains the result of the original method
}

```

## Restrictions
This module does not work and is not supported for stores using the following domain extensions: `.ru`,`.рф`,`.рус`,`.by`,`.бел`,`.su`. A part of code is encrypted for this reason.

## Download
You can download the latest version of the Library Decorator module from the following links:
- [OpenCart 3.x](https://github.com/ocmod-space/ocmod-library-decorator/raw/refs/heads/main/module/zip/3/library_decorator.ocmod.zip) version.
- [OpenCart 4.x](https://github.com/ocmod-space/ocmod-library-decorator/raw/refs/heads/main/module/zip/4/library_decorator.ocmod.zip) version.

## License
Licensed under the [MIT License](../LICENSE.txt)

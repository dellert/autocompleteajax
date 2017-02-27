# autocompleteajax
materializecss autocomplete with ajax data load

Here you can send ajax & get data with ajax, set delay and min input value length if you need, can set custom data for send request & cal callback function if need

usage example code:

```js
var $street_select = $('.js-street-select');
var $street_preloader = $('.js-street-preloader');
var initial_address;

function getStreetAutocompleteObject() {
    return {
        ajax: {
            url: $street_select.attr('data-url'),
            method: 'post',
            dataType: 'json',
            beforeSend: function () {
                if (!$street_preloader.hasClass('active')) {
                    $street_preloader.addClass('active');
                }
            },
            error: null
        },
        callback: function (res) {
            if ($street_preloader.hasClass('active')) {
                $street_preloader.removeClass('active');
            }
        },
        minLength: 2,
        delay: 200
    };
}

$street_select.autocomplete(getStreetAutocompleteObject());
```

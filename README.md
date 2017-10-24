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

$street_select.autocompleteajax(getStreetAutocompleteObject());
```

```html
<div class="input-field col s12 m12 l4">
  <div style="position: relative">
      <div class="preloader-wrapper small js-street-preloader" style="width: 20px; height: 20px; position: absolute; right: 0; margin-top: 15px">
          <div class="spinner-layer spinner-blue-only">
              <div class="circle-clipper left">
                  <div class="circle"></div>
              </div><div class="gap-patch">
                  <div class="circle"></div>
              </div><div class="circle-clipper right">
                  <div class="circle"></div>
              </div>
          </div>
      </div>
  </div>
  <input id="street"
         type="text"
         autocomplete="off"
         name="street"
         placeholder="Enter something..."
         data-url="/ajax/url-get-data"
         class="js-street-select">
  <label id="street_label" for="street" style="width: 100%">Street</label>
  <input type="hidden" class="autocomplete-id" name="autocomplete-id" value="">
</div>
```

Ajax response format from server must be like this

```js
{
    "status": 200,
    "data":[{
        id: 12,
        value: "value"
    }]
}
```

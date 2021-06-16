|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| javascript-on-submit-button-persist | javascript  | javascript, forms, css  | 20210616111452 |

# javascript on submit button persist
When working through a forms change I found it difficult to persist a slider's
animations after form submission. The implementation and sources for this are below.

[JavaScript for checkbox on change submit](https://stackoverflow.com/a/10602540)
[HTML and CSS for the slider](https://www.cssscript.com/realistic-ios-switch-pure-css/)
[Persisting the CSS state for the slider](https://stackoverflow.com/a/22125401)

The HTML for a slider:
```html
<label class="form-switch">
  <input type="checkbox">
  <i></i>
  Select Me
</label>
```

The CSS for the slider:
```css
.form-switch {
  display: inline-block;
  cursor: pointer;
  -webkit-tap-highlight-color: transparent;
}

.form-switch i {
  position: relative;
  display: inline-block;
  margin-right: .5rem;
  width: 46px;
  height: 26px;
  background-color: #e6e6e6;
  border-radius: 23px;
  vertical-align: text-bottom;
  transition: all 0.3s linear;
}

.form-switch i::before {
  content: "";
  position: absolute;
  left: 0;
  width: 42px;
  height: 22px;
  background-color: #fff;
  border-radius: 11px;
  transform: translate3d(2px, 2px, 0) scale3d(1, 1, 1);
  transition: all 0.25s linear;
}

.form-switch i::after {
  content: "";
  position: absolute;
  left: 0;
  width: 22px;
  height: 22px;
  background-color: #fff;
  border-radius: 11px;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.24);
  transform: translate3d(2px, 2px, 0);
  transition: all 0.2s ease-in-out;
}

.form-switch:active i::after {
  width: 28px;
  transform: translate3d(2px, 2px, 0);
}

.form-switch:active input:checked + i::after { transform: translate3d(16px, 2px, 0); }

.form-switch input { display: none; }

.form-switch input:checked + i { background-color: #4BD763; }

.form-switch input:checked + i::before { transform: translate3d(18px, 2px, 0) scale3d(0, 0, 0); }

.form-switch input:checked + i::after { transform: translate3d(22px, 2px, 0); }
```

Persistent JS and on change submit:
```javascript
$(document).ready(function(){
    $("#formname").on("change", "input:checkbox", function(){
        $("#formname").submit();
    });
});

$(function(){
    var slider = localStorage.input === 'true'? true: false;
    $('input').prop('checked', slider || false);
});

$('input').on('change', function() {
    localStorage.input = $(this).is(':checked');
    console.log($(this).is(':checked'));
});
```

---
layout: post
title:  "Angular Forms"
date:   2015-06-22 19:48:12
categories: angularjs forms
---
A form is an instance of *[https://docs.angularjs.org/api/ng/type/form.FormController](FormController)*. The form instance can optionally be published into the scope using the *name* attribute.

Similarly, an input control that has the *ngModel* directive holds an instance of *NgModelController*. Such a control instance can be published as a property of the form instance using the name attribute on the input control. The name attribute specifies the name of the property on the form instance.

## Using CSS classes

* **ng-valid**: the model is valid
* **ng-invalid**: the model is invalid
* **ng-valid-[key]**: for each valid key added by $setValidity
* **ng-invalid-[key]**: for each invalid key added by $setValidity
* **ng-pristine**: the control hasn't been interacted with yet
* **ng-dirty**: the control has been interacted with
* **ng-touched**: the control has been blurred
* **ng-untouched**: the control hasn't been blurred
* **ng-pending**: any $asyncValidators are unfulfilled

## Validation Techniquess

* Type Attribute (e.g. type="email")
* Required Attribute (required)
* Angular Validation Attributes (e.g. ng-minlength)
* Custom Angular Directive (the best for complex validations; e.g. my-directive="")
* Code in the Controller (Not recommended)

## Marking Invalid Elements

* ngClass Directive
* Bootstrap Styles
* Angular Validation States

```
ng-class="{'has-error': productForm.inputProductName.$invalid}"
```

### Angular Validation States

* $pristine: Entry has not been changed
* $dirty: Entry has been changed
* $valid: Entry is valid
* $invalid: Entry is invalid
* $error: All validations and whether they are valid or invalid

#### Conditions

* Form must have a name
* Input element must have a name
* Input element must include ngModel

## Display Validation Messages

* Alert Box (not a good idea)
* Validation Message Area
* Adjacent to the input element

### Displaying the Validation Messages

```
<span class="help-block has-error" ng-show="productForm.inputProductName.$invalid">Product name is required</span>
```

### Angular Validation Directives

* ng-minlength
* ng-maxlength
* ng-pattern
* ng-change

### Multiple Validation Messages -> ngMessages

```
<span ng-messages="productForm.inputProductName.$error" role="alert">
    <span ng-message="required">Proudct name is required</span>
    <span ng-message="minlength">Must be at least 4 chars in length.</span>
    <span ng-message="maxlength">Cannot exceed 12 chars in length.</span>
</span>
```

or with **ng-show**

```
<span ng-show="productForm.inputProductName.$error.required">Product name is required.</span>
<span ng-show="productForm.inputProductName.$error.minglength">Must be at least 4 chars in length.</span>
```

### Preventing the Submission

* Disable the Save Button
* Display a message

```
ng-disabled="productForm.$invalid"
ng-click="vm.submit(productForm.$valid)"
```


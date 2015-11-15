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

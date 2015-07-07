---
layout: post
title:  "ng-file"
date:   2015-05-14 11:00:00
categories: javascript angularjs
---

[The whole post](http://stackoverflow.com/questions/17063000/ng-model-for-input-type-file)

I created a workaround with directive:

{% highlight javascript %}
.directive("fileread", [function () {
    return {
        scope: {
            fileread: "="
        },
        link: function (scope, element, attributes) {
            element.bind("change", function (changeEvent) {
                var reader = new FileReader();
                reader.onload = function (loadEvent) {
                    scope.$apply(function () {
                        scope.fileread = loadEvent.target.result;
                    });
                }
                reader.readAsDataURL(changeEvent.target.files[0]);
            });
        }
    }
}]);
{% endhighlight %}

And the input tag becomes:

{% highlight javascript %}
<input type="file" fileread="vm.uploadme" />
Or if just the file definition is needed:

.directive("fileread", [function () {
    return {
        scope: {
            fileread: "="
        },
        link: function (scope, element, attributes) {
            element.bind("change", function (changeEvent) {
                scope.$apply(function () {
                    scope.fileread = changeEvent.target.files[0];
                    // or all selected files:
                    // scope.fileread = changeEvent.target.files;
                });
            });
        }
    }
}]);
{% endhighlight %}
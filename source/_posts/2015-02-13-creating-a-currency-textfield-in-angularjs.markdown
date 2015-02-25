---
layout: post
title: "Creating a currency textfield in AngularJS"
date: 2015-02-13 17:12:29 +0100
comments: true
categories: 
---

When working with currencies I have the tendency to store
the value in the database as an INT value, to encounter less rounding errors.
The value shown is 99.99 while the persisted value is 9999.

AngularJS Directive seems to be a great way to make a custom textfield.


    {% highlight ruby %}
    app.directive("currencyField",['$sce',function($sce) {
      return {
        restrict: 'AE',
        require: 'ngModel',
        template: '<input type="text" min="0.0" step="0.01" size="4" />',
        replace: true,
        link: function(scope,elem,attrs,ngModel) {
          if (!ngModel) return;

          function centsToEuro(value) {
            return value / 100.0;
          }

          function euroToCents(value) {
            return parseInt(value * 100);
          }

          ngModel.$parsers.push(euroToCents);
          ngModel.$formatters.push(centsToEuro);
        }
      }
    }]);
    {% endhighlight %}


To use it, just add currency-field to input field

    {% highlight html %}
    <input currency-field ng-model="saleitem.price" ng-blur="update(saleitem)" placeholder="price" />
    {% endhighlight %}

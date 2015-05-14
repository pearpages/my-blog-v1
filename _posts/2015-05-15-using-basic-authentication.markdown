---
layout: post
title:  "Basic Authentication"
date:   2015-05-15 09:33:15
categories: authentication javascript angularjs
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Once the user provices valid user credentials, the AngularJS application can store those credentials in a *cookie* or some other temporary storage.

All moden browsers store cookies mapped to a particular domain. Cookie access is then granted only to the application that actually created the cookie on that particular domain.

## Factory

{% highlight javascript %}
angular.module('yoAngBlogApp')
 .factory('Credentials', ['$cookies',function ($cookies) {

  return {
    check:function (){
      var returnVal = false;
      var creds = $cookies.credentials;
      if(creds !== undefined && creds !== ""){
        returnVal = true;
      }

      return returnVal;
    },
    set:function(username, password){
      var token = username.concat(":",password);

      $cookies.credentials = token;
      $cookies.username = username;
    },
    delete: function (){
      $cookies.credentials = "";
      $cookies.username = "";  
    },
    getToken: function (){
      var returnVal = "";
      var creds = $cookies.credentials;
      if(creds !== undefined && creds !== ""){
        returnVal = btoa(creds);
      }
      return returnVal;
    },
    getUsername: function (){
      var returnVal = '';
      var username = $cookies.username;
      if(username !== undefined && username !== ""){
        returnVal = unsername;
      }
      return returnVal;
    }
  };
}]);
{% endhighlight %}

## Controller

{% highlight javascript %}
angular.module('myApp')
  .controller('NewPostCtrl',['$scope','$http','$location','Credentials','blogPost',function ($scope,$http,$location,Credentials,myResource) {
    
    $http.defaults.headers.common['Authorization'] = 'Basic' + Credentials.getToken();

    myResource.save({},
        function success(response){
            $scope.status = response;
            },
        function error(errorResponse){
            console.log('Error: ' + errorResponse);
            });
  }]);
{% endhighlight %}
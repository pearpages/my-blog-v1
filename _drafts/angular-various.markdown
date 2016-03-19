---
layout: post
title: "title"
categories: category1 category2
date:  2015-05-26 19:40:22
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}


//Controller

'use strict';

/**
 * @ngdoc function
 * @name intelligenceApp.controller:SubmissionviewCtrl
 * @description
 * # SubmissionviewCtrl
 * Controller of the intelligenceApp
 */
angular.module('intelligenceApp')
  .controller('SubmissionviewCtrl', function ($scope, $routeParams,Submission,login,$location) {
          if(!login.hasSettings()){
                  $location.path('/settings');
                }
                
           $scope.id = $routeParams.id;
           var entry = Submission.get({ id: $routeParams.id }, function() {
                console.log(entry);
                $scope.submission = entry;
           },function(){
                $scope.submission = null;
           });
  });


//view

<div  ng-show="submission !== null">
        <h3>Submission details</h3>
        
        <dl>
                <dt>QuoteID</dt>
                <dd>{{submission.QuoteID}}</dd>
                <dt>ProducerID</dt>
                <dd>{{submission.ProducerID}}</dd>
                <dt>NamedInsured</dt>
                <dd>{{submission.NamedInsured}}</dd>
                <dt>Renewal</dt>
                <dd>{{submission.Renewal}}</dd>
                <dt>PolicyID</dt>
                <dd>{{submission.PolicyID}}</dd>
                <dt>InsuredID</dt>
                <dd>{{submission.InsuredID}}</dd>
                <dt>Bound</dt>
                <dd>{{submission.Bound}}</dd>
                <dt>AcctExec</dt>
                <dd>{{submission.AcctExec}}</dd>
                <dt>BndPremium</dt>
                <dd>{{submission.BndPremium}}</dd>
        </dl>

</div>

<div  ng-show="submission === null">
        <h3>Submission details</h3>
        
        <p>The submission with <strong>{{id}}</strong> does not exist.</p>

</div>
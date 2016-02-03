(function(currentScriptPath) {
    'use strict';

    angular.module("mandatory")
        .directive('dropdownButton', ['$sce',dropdownButton]);

    function dropdownButton($sce) {
        return {
            restrict: 'E',
            bindToController: true,
            controllerAs: 'vmd',
            controller: controller,
            scope: {
                options: '=',
                current: '=',
                onMyChange: '&'
            },
            templateUrl: currentScriptPath.replace('dropdown-button.directive.js', 'dropdown-button.html'),
        };

        //call ang-link if needed

        function controller() {

            var vmd = this;
            vmd.render = render;
            vmd.changeValue = changeValue;

            function render(html) {
                return $sce.trustAsHtml(html);
            }

            function changeValue(value) {
                vmd.onMyChange({value:value});
            }
        }
    }
})((function currentScriptPath() {
    var scripts = document.getElementsByTagName("script");
    var currentScriptPath = scripts[scripts.length - 1].src;
    return currentScriptPath;
})());

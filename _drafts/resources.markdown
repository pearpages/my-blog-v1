 $scope.find = function () {
                        Submission.get({id: $scope.id}, function (submission) {
                                $scope.submission = submission;
                                $scope.message = 'Submission ' + $scope.id + ' found in the server.';
                        }, function () {
                                $scope.submission = null;
                                $scope.message = 'Submission ' + $scope.id + ' NOT found in the server.';
                        });
                        console.log($scope.submission);
                };
                $scope.removeAll = function () {
                        $scope.all = null;
                };
                $scope.delete = function () {
                        Submission.delete({id: $scope.submission.QuoteID}, function () {
                                $scope.message = 'Submission ' + $scope.id + ' DELETED in the server.';
                                $scope.submission = null;
                        },
                                function () {
                                        $scope.message = 'Error deleting. The Submission ' + $scope.id + ' might not exist.';
                                });

                };
                $scope.update = function () {
                        Submission.update({id: $scope.id}, $scope.submission, function () {
                                console.log('here');
                                $scope.message = 'Submission ' + $scope.id + ' has been UPDATED in the server.';
                        }, function () {
                                console.log('theeeere');
                                $scope.message = 'Submission ' + $scope.id + ' NOT FOUND in the server.';
                        });
                };
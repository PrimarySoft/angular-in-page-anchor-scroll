# angular-in-page-anchor-scroll
A quick and easy function activating in-page (html) anchor scrolling.  Can be easily integrated into your html BODY controller to activate.  No change to how you write anchors in HTML and adds a simple function to activate the functionality.


In your HTML, write all of your anchors exactly as you would with standard HTML4/HTML5

<h1 id=“SomeAnchor”> My Title </h1>

In this case, the anchor is #SomeAnchor.  In CSS you could reference it using #SomeAnchor {styles: styles;}


Angular:

This project assumes that you have a page controller of some sort on <Body> or on a container div which emcompasses all of the anchors you want to use.
—EX: index.html (obviously missing html, head, js, etc.)—
<body ng-controller=“MyController”>
	<h1 id=“SomeAnchor”> My Title </h1>
</body>
———


Angular Controller — (reference: https://docs.angularjs.org/guide/controller ):

“When a Controller is attached to the DOM via the ng-controller directive, Angular will instantiate a new Controller object, using the specified Controller's constructor function. A new child scope will be created and made available as an injectable parameter to the Controller's constructor function as $scope.” — https://docs.angularjs.org/guide/controller

The following example demonstrates creating a MyController, which attaches a greeting property containing the string 'Hola!' to the $scope:

—————BEGIN CODE—————
var myApp = angular.module('myApp',[]);

myApp.controller('MyController', ['$scope', '$location', '$anchorScroll', function(t,o,l){
	//New function for anchor scroll
	t.scrollTo = function(e) { 
			o.hash(e); //change hash fragment to e (passed in via functiona call)			l.yOffset = 42; //offset height of any fixed header/nav value (px);
			l(); //Make it happen!  Execute page scroll to the hash (minus any yoffset value)
	};

}]);

—————END CODE—————


Calling it from the HTML like this:
Ex.: ng-click=“scrollTo(‘YourAnchorWithNoPoundSign’)”
Ex.: ng-click=“scrollTo(‘SomeAnchor’)”

<a ng-click=“scrollTo(‘SomeAnchor’)”>Scroll to SomeAnchor</a>




Full working example:
<html>
<head>
<style>
div {height:700px;}
</style>
<!— remember to add your angular and reference your controller js —>
<script>
var myApp = angular.module('myApp',[]);

myApp.controller('MyController', ['$scope', '$location', '$anchorScroll', function(t,o,l){
	//New function for anchor scroll
	t.scrollTo = function(e) { 
			o.hash(e); //change hash fragment to e (passed in via functiona call)			l.yOffset = 42; //offset height of any fixed header/nav value (px);
			l(); //Make it happen!  Execute page scroll to the hash (minus any yoffset value)
	};

}]);
</script>
</head>
<body ng-controller=“MyController”>
	<div><h1 id=“SomeAnchor”> First Anchor </h1><p><a ng-click=“scrollTo(‘NextAnchor’)”>Scroll to NextAnchor</a></p></div>
	<div><h1 id=“NextAnchor”> Last anchor </h1><p><a ng-click=“scrollTo(‘SomeAnchor’)”>Scroll to SomeAnchor</a></p></div>
</body>
</html>







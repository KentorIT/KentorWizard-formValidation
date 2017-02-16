#KentorWizard-formValidation

####` PM> Install-Package Kentor.jQueryWizardFormValidation`

####` bower install KentorWizard-formValidation`

##Description 
This wizard provides form validation and basic wizard functionality such as next and previous step buttons and breadcrumb navigation. 
####Breadcrumbs
To use breadcrumb navigation simply use the class `<div class="wizard-breadcrumb"></div>`. The breadcrumb link text is, if not undefined, retrived from the ´data-step-header´ else it will display the step number. 
##HTML
####A basic HTML example
```html
<head>
    <meta charset="utf-8"/>
    <title>Kentor Wizard Exemple</title>
    //using NuGet
    <script src="Scripts/jquery-1.10.2.js"></script>
    <script src="Scripts/jquery-validate.js"></script>
    <script src="Scripts/Kentor/wizard.js"></script>
    <script src="Scripts/Kentor/validate.js"></script>

    //using Bower
    <script src="bower_components/jquery/jquery.js"></script>
    <script src="bower_components/jquery-validation/jquery.validate.js"></script>
    <script src="bower_components/KentorWizard/js/wizard.js"></script>
    <script src="bower_components/KentorWizard-formValidation/js/validate.js"></script> 
<body>
    <div>
        <form id="target" action="index.html">
            <div class="wizard" data-forward-button-text="Next">
                <div class="wizard-title-wrapper page-title-divider">
                    <div class="wizard-title"></div>
                </div>
                <div class="wizard-header">
                    <div class="wizard-step-label"></div>
                    <div class="wizard-info"></div>
                </div>
                <div class="wizard-step">
                    <input type="text" required>
                </div>
                <div id="000" class="wizard-step">
                    <input type="text" required>
                </div>
                <div class="wizard-step" data-step-header="Preview" data-forward-button-text="Send">
                    <p>333333333333333333333</p>
                </div>
                <div class="wizard-footer">
                    <div class="wizard-back">
                        <button type="button" class="cancel wizard-back-button">Back</button>
                    </div>
                    <div class="wizard-breadcrumb"></div>
                    <div class="wizard-forward">
                        <button type="button" class="wizard-forward-button">Next</button>
                    </div>
                    <div class="wizard-message-area"></div>
                </div>
            </div>
        </form>
    </div>
</body>

```
##JavaScript
 The wizard takes an object as an argument which enables the possibility to "overload" some wizard functions. 

####Without an argument these default options will take effect
```javascript
 var defaultOpts = {
 	nextHandler: function(event) {}, 
	onloadHandler: function(event) {}, 
	backHandler: function(event) {}, 
	wizardStepRendered: function (event) { }, 
	stepText: "Step {0} of {1}", 
	shiftAnimationHide: function (stepToHide) { stepToHide.hide(); }, 
	shiftAnimationShow: function (stepToShow) { stepToShow.show(); }, 
	breadcrumbDivider: " | ", 
	focusFirst: true, 
	validationFalseHandler: function (validator) {
                console.log(validator);
                return;
            }
	}
```
####An example on how to "overload" the wizard options
```javascript
$(this).wizardFormValidation({
			
		//This function is called when .wizard-forward-button is clicked.  
           nextHandler: function(event) {
			 if(event.IsLastPage) { 
				 $(this).closest("form").submit();
			 }
		   }
        //This function is called when loading the wizard.                
           onloadHandler: function(event) {
           alert("Loading wizard")
           },
		//This function is called when .wizard-back-button is clicked.
           backHandler: function(event) {
           alert("You are now going to the previous step")
           },
		//This is set to .wizard-step-label. To change language set stepText. 
           stepText: "Steg {0} av {1}",
		//This function is called to hide the previous step.
           shiftAnimationHide: function (stepToHide) { stepToHide.slideUp(); },
		//This function is called to show the next step.
           shiftAnimationShow: function (stepToShow) { stepToShow.slideDown(); },
		   //This is set between breadcrumb buttons
		    breadcrumbDivider: "<<<<>>>>>",
	   //When a step is rendered the wizard will as default if a form is used focus on the first input
	   focusFirst: false, 
	   //If form is not valid this function vill be called
	   validationFalseHandler: function (validator) {
                console.log(validator);
                return;
            }
           
});
```

## More Examples

###Add a new button
####HTML
```html
<div class="wizard-footer">
	<div class="myWizard-doSomething">
		<button type="button" class="myWizard-doSomething-button">Save</button>
	</div>
</div>
```
####JavaScript

```javascript
$.fn.extend({
	
	myWizard: function (myDoSomethingHandler, options) {
		
		$(this).find("myWizard-doSomething-button").click(function (event) {
			if(myDoSomethingHandler !== null) {
				myDoSomethingHandler(event);
			}
		});
		
		$(this).wizardFormValidation(options);
		
	},

});
```
###Navigation

```javascript
myWizard.goWizardStep(number);
myWizard.goWizardStep("#id");
myWizard.goWizardNext();
myWizard.goWizardBack();

myWizard.wizardFormValidation().goWizardStep(number);
myWizard.wizardFormValidation().goWizardStep("#id");
myWizard.wizardFormValidation().goWizardNext();
myWizard.wizardFormValidation().goWizardBack();

```

####Use breadcrumbs with bootstrap example

```html
<div class="wizard-breadcrumb"></div>
```

```javascript
onloadHandler: function () {
	$(.wizard-breadcrumb).addClass("row");
	$(.wizard-breadcrumb-button).addClass("col-md-4");
	
}

```

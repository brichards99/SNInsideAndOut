A common requirement for Service Portal developers is to slightly modify elements on a widget to meet some nuanced need. It may be as simple as adding extra text next to a field on a form or perhaps a more complicated bit of functionality, such as a customized button on a catalog item form.

Generally speaking, it is considered to best practice to avoid modifying out of the box widgets. Put differently, using out of the box widgets 'as-is' helps to reduce technical debt associated with customizing the Service Portal. Either way, it's easy to get into the weeds pretty quickly when going the clone-it-and-twiddle approach, and very often there are easier ways. The options for introducing changes are several:

1. Start by investigating UI policies and client scripts that can produce the desired changes. Keep in mind that it is usually possible to build a specific view for Service Portal interactions, and these views can be targeted by well known tools such as these.
2. Investigate widget options and URL parameters that might affect the behavior of the widget. This requires a careful analysis of the OOB widget code, but it can sometimes reveal behavior not necessarily apparent when simply looking at the option schema. An example: have you looked into events broadcast by the Simple List widget when an item is clicked?
3. Add a custom widget to the portal page that can affect the behavior or appearence of the OOB widget in the exact context (the page) where customization is needed, but not elsewhere. This is the purpose of this article.

By the way, another best practice for Service Portal development is to avoid manipulating DOM elements on the page to achieve desired outcomes. One good reason for this is the elaborate hierarchical structure of a portal page. Playing around with the DOM in a given widget might have unintended consequences for other widgets on the page.  The spirit behind this best practice is one reason why JQuery is not commonly recommended for widget development.

I would say, however, that if you know exactly what you want to do and limit the scope of what you're doing very specifically then any tool is fair game. And JQuery can be pretty powerful.

Let's do this: add an icon next the breadcrumbs on the Order Status portal page. Kind of a weird thing to do, but it will demonstrate the point.

The techncial strategy we will employ in our custom widget is as follows:

* Wait for all the HTML on the page to render.
* Find the very specific element we want to insert our icon after.
* Plop in the HTML for that icon using JQuery.

To make this happen, we need to identify the exact HTML to search for. Navigate through the portal to the desired page and simply right-click and 'view source' (or 'inspect'). Doing so we find this:

<ul class="nav nav-pills nav-sm"> 
  <li> <span><a ng-href="?id=index" href="?id=index">Home</a> <i aria-hidden="true" class="fa fa-chevron-right"></i></span> </li> 
  <!-- ngIf: !c.expanded && c.breadcrumbs && c.breadcrumbs.length > 2 --> 
  <!-- ngIf: !c.breadcrumbs --><li ng-if="!c.breadcrumbs" class="ng-scope"><span><a style="display: inline;" class="a-disabled ng-binding" aria-current="page" href="">Order Status</a></span></li><!-- end ngIf: !c.breadcrumbs --> 
  <!-- ngRepeat: item in c.breadcrumbs track by $index --> 
 </ul>

This widget will use the $JQuery method '.after' (check out the API at https://api.jquery.com/after/), and for this the syntax we need is basically what you would use for targeting an element in CSS. Looking at the code above, we will write our target element as follows:

ul.nav-pills > li > span > a.a-disabled

This exact sequence of elements using class names is something we can be pretty sure won't appear elsewhere on the page. Finding the target here can require a bit of creative problem solving, and it may not work for every situation or need. One thing that is clear right away is that we cannot inject class names or parameters within an element. We're just inserting something new between elements, as it were. If you spend a little time looking through the JQuery API you may find a few more interesting things to do.

WIth the target identified we need the code we want to insert:

<i class='fa fa-forward'></i>

Note that this is a complete tag, with starting and ending elements. (I just picked icon for the purposes of this demonstration even though it might not actually make sense.)

We now can build a custom widget where we will use only the client script to work our magic.


Name: Insert Custom Icon
ID: custom-icon

Body HTML: <leave alone>
CSS: <leave alone>
Server script: <leave alone>
Client script:

function() {
    /* widget controller */
    var c = this;

    function waitForElements(selector, callback) {
        var poller1 = setInterval(function() {
            $jObject = jQuery(selector);
            if ($jObject.length < 1) {
                return;
            }
            clearInterval(poller1);
            callback($jObject);
        }, 100);
    }

    function addCustomCode($jObject) {
        var newIcon = "<i class='fa fa-forward '></i>";
        $jObject.after(newIcon);
    }

    var targetElement = "ul.nav-pills > li > span > a.a-disabled";

    waitForElements(targetElement, addCustomCode);

}
Now all that is required is that we drop this widget onto the page where we want the breadcrumbs to be updated. 

Some things that are worth noting about using this approach:

* Adding a widget customization in this manner is very quick and easy to revert -- as opposed to a cloned-and-modified OOB widget, which would require more maintenance.

* Single-purpose custom widgets built for things like this are ideal for self-documentation, either simply in the widget name or in the server / client script sections of the widget.

* Because you have an entire custom widget to fiddle with, it is possible to make this behavior conditional. Using the Server script, for example, you could determine if the user has a certain role, for example, and wrap the 'waitForElements()' call at the bottom of the client script in an IF statement.

* It is possible to make the code inserted interact with client / server scripts. To do so it is necessary to add the desired scripts to the custom widget and make use of $scope.
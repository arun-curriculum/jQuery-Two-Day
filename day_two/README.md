#jQuery Part 2

##Front-End Templating with Handlebars
- Handlebars is a front-end templating framework.
- Think of EJS or ERB, for the front end.
- Basically, you will need a templating framework any time you have a collection of data and you want to display it in some specified way.
- Handlebars is really good at taking JSON data and displaying it.

####Setup
- Download the [Handlebars library](http://handlebarsjs.com/).
- Download [JSONView Chrome plugin](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en).

####AJAX Refresher
- For today's lesson we will be using jQuery to handle the AJAX calls.
- AJAX is a way to send and receive data from the server asynchronously from the page load.
- The syntax for jQuery AJAX is as follows:

```
$.ajax({
	url: "YOUR ENDPOINT HERE",
	type: "GET",
	success: function(data) { },
	error: function(jqXHR, textStatus, errorThrown) { }
});
```

####How to Use Handlebars
- Handlebars templates are handled through `<script>` tags, which allow them to be ignored while rendering the page:

```
<script id="my-template" type="text/x-handlebars-template">
```

- You can write any normal HTML here, but you can also write Handlebars-specific code:

```
<script id="my-template" type="text/x-handlebars-template">
	<div class="entry">
		<h1>{{title}}</h1>
		<div class="body">
			{{body}}
		</div>
	</div>
</script>
```

- The curly code is essentially keys to a JSON object.
- If you need to, you can also loop through an array of JSON objects to produce very dynamic templates. You will do this today. Here is an example from the docs on how this can be done through helpers:

```
<h1>Comments</h1>

<div id="comments">
	{{#each comments}}
		<h2><a href="/posts/{{id}}">{{title}}</a></h2>
		<div>{{body}}</div>
	{{/each}}
</div>
```

- This example assumes that `comments` is an array of JSON objects.

- Before a template is used however, it must be first "compiled":

```
var source   = $("#my-template").html();
var template = Handlebars.compile(source);
```

- The function `Handlebars.compile` returns a function that can be passed JSON data as an argument.
- This resulting function returns HTML after the JSON data is processed into it.
- You can then apply your template anywhere you need to:

```
var jsonData = {
	title: "My New Post",
	body: "This is my first post!"
};

var template_html = template(jsonData);
$("#some-div").html(template_html);
```

##Book Manager with Handlebars
- We will be creating a simple book manager system using handlebars to take care of the templating.
- The API for this exercise will be `http://daretodiscover.herokuapp.com/books`.
- Here are the API endpoints:
	- `GET /books` -> Get all books
	- `POST /books` -> Create new book
	- `GET /books/:id` -> Get a specific book
	- `PUT /books/:id` -> Update a book
	- `DELETE /books/:id` -> Delete a book

##Introduction to jQuery UI
- jQuery UI is a library that extends the functionality of jQuery core.
- jQuery UI wraps in powerful feature including dynamic UI elements, more effects and easings, and drag and drop support.
- Let's try out some of the neat things it can do by implementing some of the widgets.

##Build Me jQuery Form Exercise
- In this exercise we will be combining our knowledge of jQuery core with jQuery UI to build a dynamic form.
- You can find the files for this exercise [here](jquery_form/).
- Here are the rules:
	- When full name is filled out it should populate the name card automagically.
	- About yourself cannot be more than 140 characters long.
	- Day you are free needs to use the jQuery UI datepicker.
	- How much money should use the jQuery UI slider.
	- When everything is filled out, form should be submitted using AJAX to `http://daretodiscover.herokuapp.com/form`.
	- **Bonus:** As you go through the form you should include a jQuery UI progress bar at the top that updates automatically.
	- **Bonus:** As you go through the form have the background color of the page animate between a few subtle colors.
## API Design - Subscribe & Save Service

This activity will explore designing and implementing operations for the Subscribe & Save Service. With Subscribe & Save customers can set up regularly scheduled deliveries and earn savings. Customers save 5% on all subscriptions, but if they receive five or more products in one auto-delivery they save 15% off all items in that delivery. From diapers to toothpaste to dog treats, customers can subscribe to thousands of everyday products.

### Install and Run

This project does not require compiling, so feel free to open the project up in any text editor of your choosing (IntelliJ is a perfectly acceptable option here). 

Before you start, try opening the `index.html` file in the browser. It should show you a functioning page with some API documentation.

We will be using the following steps in our Code-Along. Feel free to follow along.

### PART A - Add a subscription!

Until a customer can sign up for a subscription, our service is pretty useless. Let’s get started defining our first operation. The OpenAPI model will be defined in the model/classroom/subscribeAndSave/ directory of your past Subscribe and Save project.

Let’s dive into the AddSubscription operation and motivate it with a use case:

- As a customer, I want to add a subscription, so that I can get a discount and so that it will show up automatically at my door on a frequency I set.

Requirements:

- If the system encounters an unexpected error while processing a request, it will return a service error.
- If a userId, asin, quantity, or monthly frequency is not provided, return a client exception.
- The next shipment month will be determined by the service based on the current date and customer’s requested frequency of subscription
- This operation will need subscription data as a part of its input to satisfy this use case. Let’s say it also returns the subscription. That way the customer gets confirmation that their subscription was added how they intended.

Let’s start off by defining the Subscription object. Each of the Subscription members are listed in the table below. For each member fill in the data type that should be used and if any traits should be applied. We’ll define these types when we add the operation.

| name   |  type | is required? |
|--------|-------|-------|
|userId|String|yes|
|asin|||
|quantity|||
|monthlyFrequency|||
|nextShipmentMonth|||

For this operation, we’ll define the URI as /subscriptions/users/{userId}/products/{asin} and use the PUT verb. 
- Why do you think we should use PUT here instead of a POST?
- Are there any fields of the Subscription object that clients shouldn’t send as a part of the request?
- What fields should the request parameters include?
- What fields should our response object have?

#### Extension
- What other use cases might you need to support?
- List additional APIs you would develop to address these use cases.

### PART B - Define add a subscription

Now, we will be adding our operation to add a subscription to our model definition. Using editor.swagger.io, you can validate your code as you write a new operation. Here are a few steps to help you think through how to define a new operation.

#### Steps for defining your model:
1. Declare the new operation’s endpoint/path.
    1. Add a new operation object with its path, without any input, output, or errors in your file
    1. Determine the HTTP method name for your operation (GET, PUT, POST, etc)
    1. Write out the description of what you want this operation to do.
1. Declare the inputs and outputs.
    1. Define the parameters inside your operation. These parameters should be limited to what your service needs to complete the operation.
    1. Similarly, define the output. If the output is an object (as opposed to a single field), add a new object structure to your component’s schema.
1. Update your operation’s path if needed
    1. If a parameter should be passed in the path, update your path so it has a placeholder for your parameter.
1. Define your errors.
    1. Add any errors to the operation.

### PART C - List all subscriptions for a user

Review the following use case and its requirements:

**Use Case:** As a customer, I want to see all of my subscriptions. 

**Requirements: **

- If the system encounters an unexpected error while processing a request, it will return a service error.
- If a customer doesn’t have any subscriptions, return a user not found exception.

1. Choose a path for your new operation.
1. What HTTP verb will you use?
1. Write the description of what the operation will do
1. Are any values required to fulfill this operation?
1. What value/s should the service return in its response?
1. List which exceptions should be returned from this operation and when.

### PART D - Creating the RapiDoc page

Using editor.swagger.io, you can export your file as JSON by going to File > Convert and save as JSON.

 ![img1](/img1.png)

RapiDocs only support JSON, but thankfully, we can write our code in YAML and export it as JSON without having to rewrite it.

Your GitHub project already has a basic RapiDoc HTML document (index.html) that you can use to load and see your documentation. Save your YAML file in the same folder. Now open the RapiDoc file in your browser and load your JSON file into the document. You should see your documentation.

### PART E - Making your API Doc Publically Available

With your document in hand, upload your JSON file to a public S3 folder. Once it’s uploaded, copy the URL for that file and add it to your index.html file in the tag api-doc and assign it to the spec-url key. If you try to reload your index.html file from your machine, you should see the URL at the top of the page, but the documentation won’t load. This is expected and its the state that we want this to be in at this moment.

Now upload your index.html file into the same S3 bucket as your JSON file. Once that’s uploaded, find it’s URL and open that page. You should now see your page load your documentation. Try sending your link to someone else and see if they can load your page as well. If they can, you have successfully made your API documentation public.

#### Extension

As our subscriptionDao gets bigger, the list operation will need to return more and more data. If we imagine a frontend client, they may only want to list 20 results on a page. This way of breaking up data for users requires us to use pagination. Look up ways to implement pagination in REST APIs and see if you can implement it here.



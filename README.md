### The first part of the test is a web page listing all the available brokers from the BrazilAPI
In the end of this document, there is the JSON Flow of all the project to copy and paste on node-red import option.

The first thing to do, is to open a node-red locally running server on the terminal by tipying "node-red", like the example bellow:

![alt text](Files/terminal.png)

Then, you need to copy the URL of the local server in the terminal and paste it on the browser: 

![alt text](Files/server.png)

When the node-red server load in your browser, you will need four nodes connected:

http in ---> http request ---> function ---> http response

 like the example bellow:

![alt text](Files/NodeFlow.png)

Now, you need to do the node configuration:

Node 1: http in

![alt text](Files/Node1.png)

Node 2: http request

![alt text](Files/Node2.png)

Node 3: function

Set the function to "On message" and paste the code below:

[Function code](Files/code.txt)

Node 4: http response

![alt text](Files/Node4.png)


Click on deploy then access http://127.0.0.1:1880/brokers to see the web page listing all the brokers from BrazilAPI

### The second part of the test is a web page capable to show details of a provided zip code using BrazilAPI

# Option 1: Route Input (/cep/:cep)

Node 1: http in
![alt text](Files/httpin.png)

Node 2: change
![alt text](Files/change.png)

Node 3: Link out
![alt text](Files/linkout.png)

# Option 2: HTML Form(/search-cep)

Node 1: http in
![alt text](Files/httpin2.png)

Node 2: Template
![alt text](Files/template.png)

[Template code](Files/templatecode.txt)

Node 3: http response
![alt text](Files/response.png)

# Option 2: Form Processing (/submit-cep)

Node 1: http in

![alt text](Files/in.png)

Node 2: Change

![alt text](Files/changenode.png)


# API logic 

Node 1: link in

![alt text](Files/link.png)

Node 2: Function

![alt text](Files/function.png)

Node 3: http request

![alt text](Files/Request.png)

Node 4: template 

![alt text](Files/templatenode.png)

Node 5: Link Out

![alt text](Files/out.png)

Node 6: Error template

![alt text](Files/error.png)

Node 7: change node

![alt text](Files/ch.png)

Node 8: link in 

![alt text](Files/innode.png)

Node 9: http response

![alt text](Files/finalresponse.png)

JSON flow to copy and paste: [text](flow.json)
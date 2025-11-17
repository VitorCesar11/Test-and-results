### The first part of the test is a web page listing all the available brokers from the BrazilAPI
### JSON flow to copy and paste: [Flow JSON](flow.json)

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

access http://127.0.0.1:1880/search-cep to search a zip code

The final look of the project is going to be something like this:
![alt text](Files/final.png)

JSON flow to copy and paste: [Flow JSON](flow.json)

### MQTT Challenge:
I have chosen the MQTT topic to do a microservice. The service removes the need for a web-facing interface (HTTP) and instead operates entirely over the MQTT protocol. It follows an asynchronous request/response pattern.

Workflow:

Listen: The service subscribes to the MQTT topic cep/request and waits for a message (a CEP as a string) to be published.

Process: Upon receiving a CEP, the flow calls the external BrasilAPI (via an HTTP Request) to fetch the full address details.

Respond: The service formats the API's response as a JSON object and publishes it to a success topic: cep/details.

The microservice is robust and includes a dedicated path for failures. If the BrasilAPI returns an error (such as an invalid or unfound CEP), the flow catches this, formats a JSON error message, and publishes it to a separate topic: cep/error.

Node 1: mqtt in (Listen for CEP)

![alt text](Files/mqttin.png)


Node 2: change (Set msg.cep from payload)

![alt text](Files/changenod.png)

Node 3: function (Build CEP API URL)

![alt text](Files/func.png)

Node 4: http request (Call BrasilAPI CEP V2)

![alt text](Files/req.png)

Node 5: json (Convert Object -> String)

![alt text](Files/json.png)

Node 6: mqtt out (Publish Details)

![alt text](Files/mqttout.png)

Node 7: function (Format Error JSON)

![alt text](Files/errorfunc.png)

Node 8: json (Convert Object -> String)

![alt text](Files/jsonconvert.png)

Node 9: MQTT Out (publish error)

![alt text](Files/publish.png)

Example of the microservice use:

![alt text](Files/microservice.png)



How to Test the MQTT Microservice
You cannot use your browser. You must use an MQTT client, like the HiveMQ Web Client:

Go to: http://www.hivemq.com/demos/websocket-client/

Click Connect.

In the Subscriptions section, click Add New Topic Subscription and subscribe to the topic: cep/details

In the Publish section, set the Topic to: cep/request and in the Message, type a CEP: 01001000

Click Publish.

The result (the address JSON) will instantly appear in the Messages box.

### Final look of the project + MQTT Challenge:

![alt text](Files/finalook.png)



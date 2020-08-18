# ExercicioRESTful

Hospedagem
Servidor do Heroku

https://helo-word.herokuapp.com
ou
https://exerciciorestful.herokuapp.com

Requisições GET

Retornar toda lista
https://exerciciorestful.herokuapp.com/mobile/list/

Retornar um registro
https://exerciciorestful.herokuapp.com/mobile/list/2/





## DOCUMENTAÇÃO
https://phppot.com/php/php-restful-web-service/



PHP RESTful Web Service API – Part 1 – Introduction with Step-by-step Example
Last modified on February 19th, 2019.
This is part 1 of a three part series to help you learn RESTful web services using PHP. These tutorials will be comprehensive, by following it through you can build your own web services easily and consume external services.

In this tutorial, we will see how to create PHP RESTful web service without using any framework. Most of the times I do prefer to write custom code without depending on frameworks since this approach has lot of advantages. Mainly, this will take you deeper in learning the concepts and you can keep things sleek and effective.

REST or Representational State Transfer is one of the popular architectural style used to develop web services. This style of architecture contains constraints or rules to design web services which can be accessed from external apps or web applications.

The objective of this PHP RESTful web service example
The objective is to build a RESTful web service in PHP to provide resource data based on the request with the network call by the external clients. Also, the following list of steps are implemented while customizing this example without depending on any framework.

Create request URI with patterns that follow REST principles.
Make the RESTful service to be capable of responding to the requests in JSON, XML, HTML formats.
Demonstrate the use of HTTP Status code based on different scenarios.
Demonstrate the use of Request Headers.
Test the RESTful web service using a REST client.
How it is made?
An array of mobile names are the resource data that will be targeted by the REST clients. I have this resource in a domain class of this PHP RESTful example.

For accessing these data via this web service, the client will send the request by setting URI, parameters with the selected method, and more information.

The resource handlers of the web service will prepare the response in JSON, XML or HTML format based on the request. Then, the response will be sent to the client.

On the Internet, I have seen web services tutorials and most of the times they all turn out to be error-prone or incomplete. I tested those RESTful services using a REST client and mostly they fail.

view demo

What is inside?
What is RESTful?
RESTful web services vs RPC web services
RESTful web services API architecture
Uses of RESTful API
PHP RESTful web service example
File structure of RESTful example service
RESTful services URI mapping
UML sequence diagram for the example RESTful service
RESTful web service controller
A simple RESTful base class
RESTful web service handler
RESTful web service client
RESTful Web Service Output
What is RESTful?
REST stands for Representational State Transfer and it is an architectural style that enables communication between systems. The term REST was first coined by Roy T. Fielding in his PhD. dissertation.

The concept of REST is defined by certain rules, constraints or principles. The system, application, services or whatever satisfies these REST principles are called RESTful.

Web services that follow the RESTful principles are RESTful services. The URI is used to access RESTful services to get the resources.

In the RESTful glossary, the resources are nothing but the data and functions. So eventually we will call the web services via URI to access functions and thereby get the resource data.

REST Constraints
The following constraints define the RESTfulness of an application or service.

Client-Server architecture
Statelessness
Uniform interface
Layered system
Cacheability
Code on Demand
RESTful web services vs RPC web services
The following table shows the comparison of RESTful and RPC style web services. This comparison is made by factors like service request URI, request methods, data transmission, service handlers and more.

 	RESTful-Style	RPC-Style
Request URI	The request URI will differ based on the resource.	Same URI for all resources.
Request methods	The service request parameters can be sent via GET, PUT, POST request methods.	Supports only the POST method.
Service methods or handlers	Same method for all resources.	Methods and params are posted on request.
Target on	The service request using this style targets resources.	The target is methods.
Response data transmission	Over HTTP	wrapped with the requested methods and params.
RESTful web services API architecture
The following diagram shows a RESTful web service architecture. In this diagram, the request-response flow among the client-server is represented.

In this diagram, the database is shown as a resource. Based on the web service the resource can be XML feed, JSON data extracted from the file system or any.

RESTful Web Services API Architecture

Uses of RESTful API
RESTful API provides services to access resources from external applications or REST clients. Some of the predominant uses of the RESTful API is listed below.

As an interface with multi-platform support which is used to access resources from outside application coded in various programming languages like PHP, JAVA, Android and more.
REST is the simple architectural style for transmitting data over HTTP.
The REST API is the most suitable resource provider for an AJAX-based application interface which requires data to update UI without page reload.
By meeting more the REST constraints, the web applications or services can support a wide range of clients.
PHP RESTful web service example
In the PHP RESTful web service example, the following domain class contains the resource data array and service handlers. These handlers are called based on the request sent by the REST client or external apps.

In the next section, we can see all the file structure and the purpose of each file of this example.

<?php
/* 
A domain Class to demonstrate RESTful web services
*/
Class Mobile {
	
	private $mobiles = array(
		1 => 'Apple iPhone 6S',  
		2 => 'Samsung Galaxy S6',  
		3 => 'Apple iPhone 6S Plus',  			
		4 => 'LG G4',  			
		5 => 'Samsung Galaxy S6 edge',  
		6 => 'OnePlus 2');
		
	/*
		you should hookup the DAO here
	*/
	public function getAllMobile(){
		return $this->mobiles;
	}
	
	public function getMobile($id){
		
		$mobile = array($id => ($this->mobiles[$id]) ? $this->mobiles[$id] : $this->mobiles[1]);
		return $mobile;
	}	
}
?>
File structure of RESTful example service
Below file structure shows the simplicity of creating a RESTful web service example. 

As discussed above the Mobile.php is the domain class which is having resource array and handlers to get the resource.

PHP RESTful Web Service File Structure

The .htaccess file is used for mapping the request URI to the REST service endpoint.

In the following sections, we will see how the URI is mapped, how the service handler is invoked to get resource data from the domain.  – URI RFC 3986

RESTful services URI mapping
Every resource is identified via a URI (Uniform Resource Identifier). 

A Uniform Resource Identifier (URI) is a compact sequence of characters that identifies an abstract or physical resource.

RestController.php shown in the above file structure is the PHP endpoint to which the request is to be forwarded.

In this example, I provide two URIs for accessing this web service from external applications or REST client. One URI will be used to get the complete array of mobile names in a JSON format and the other is to get a particular mobile name based on the ident passed via the request URI.

URI	Method	Type	Description
http://localhost/restexample/mobile/list/	GET	JSON	To get the list of mobile names in an JSON array.
http://localhost/restexample/mobile/list/{id}/	GET	JSON	To get single mobile data array by ident passed via URL.
The following URIs are mapped to the real file via the .htaccess file.

URI to get the list of all mobiles:

http://localhost/restexample/mobile/list/
URI to get a particular mobile’s detail using its id:

In the below URI the number ‘2’ is the id of a mobile. The resource domain class can get the particular data with the reference of this id parameter.

http://localhost/restexample/mobile/list/2/
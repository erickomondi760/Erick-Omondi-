This is an implementatin demonstrating how a web application functions including but not limited to CDI producer(EntityManagerProducer.java),an entity(Product.java) ,entity fields validator(FieldValidator.java),a service bean(ProductFacade.java) and a rest endpoint(ProductRest.java).
FieldValidator.java is a class responsible for determining violated constraints on entity fields.It implements an exception mapper interface. The interface has one method that returns a response object pertaining to the violated constraint. The method accepts an argument of an exception thrown when a violation is encountered on an entity field. The violated contraint is stored in a map that is then accesed and the violation message returned to the connected client via a response object.
To register the validating class to a RESTful web service runtime,it has to be annotated with the @Provider annotation.
The entity Product.java declares a field department that is annotated with a regex pattern as a constraint. If the constraint is violated, a message relating to the constraint is built via the FieldValidator.java and returned to the client.
ProductRest.java is a restful end point of the application. FieldValidator.java is registered to the restful runtime via an annotation @Provider. On the create method, @Valid annotation is passed as one of the paramaters so that validation can occure at the restful level rather than at the persistence level. If a client application submitms an entity that violates the declared constraint, a message containing the violation is passed back.
EntityManagerProducer.java is used to produce an instance of a persistence unit once throughout the entire application. This allows for injection of the entity manager instance in any class whenever it is needed for use. It is as well annotated with the @Provider annotation to register it to the restful web service runtime.

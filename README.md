# Accessing JPA Data with Rest
This application uses Spring Data JPA to store and retrieve data on a relational database. The data is then accessed through a hypermedia based RESTful front end

Spring Data JPA focuses on using JPA to store data in a relational database. Its most compelling feature is the ability to create repository implementations automatically, at runtime, from a repository interface.

## Running the application
This application uses Maven so you can run the application by using
        
        ./mvnw spring-boot:run

## Testing the Application
Now that the application is running, you can test it. You can use any REST client you wish. Postman, Rest Client for VS Code, CURL for *nix based systems just to mention a few.

First you want to see the top level service.

    http://localhost:8080
    {
    "_links" : {
        "people" : {
        "href" : "http://localhost:8080/people{?page,size,sort}",
        "templated" : true
        }
    }
    }

The following example shows how to see the people records (none at present):

    $ curl http://localhost:8080/people
    {
    "_embedded" : {
        "people" : []
    },
    "_links" : {
        "self" : {
        "href" : "http://localhost:8080/people{?page,size,sort}",
        "templated" : true
        },
        "search" : {
        "href" : "http://localhost:8080/people/search"
        }
    },
    "page" : {
        "size" : 20,
        "totalElements" : 0,
        "totalPages" : 0,
        "number" : 0
    }
    }

Creating a new Person

    $ curl -i -H "Content-Type:application/json" -d '{"firstName": "Fredrick", "lastName": "Eric"}' http://localhost:8080/people

    HTTP/1.1 201 
    Vary: Origin, Access-Control-Request-Method, Access-Control-Request-Headers
    Location: http://localhost:8080/people/1
    Content-Length: 0
    Date: Mon, 22 Mar 2021 02:59:28 GMT
    Connection: close

Accessing a specific record

    http://localhost:8080/people/{id}

Searching for a record

    http://localhost:8080/people/search/findByLastName?name={name}

Updating a specific record: run PUT or PATCH calls at

    http://localhost:8080/people/{id}

Deleting a specific record: run a DELETE call at

    http://localhost:8080/people/{id}

# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged: 
    -I tried submitting a new toy and looked at the server logs.

![img]([https://example.com/path/to/image.jpg](https://github.com/moringa-school-labs-and-assignments/phase-4-debugging-network-requests-lab/blob/main/images/Screenshot%20from%202023-06-25%2006-55-11.png?raw=true))

    -Ahe server logs indicated that it was an internal server error and even suggested a possible fix so I tried that solution first.

    -After changing the name the request was successful and the toy was created in the database

- Update the number of likes for a toy

  - How I debugged:
    -Attempted to like a toy and looked at the server logs for any possible leads

  ![img]([https://example.com/path/to/image.jpg](https://github.com/moringa-school-labs-and-assignments/phase-4-debugging-network-requests-lab/blob/main/images/Screenshot%20from%202023-06-25%2007-05-39.png?raw=true))

    -The error log suggested that the error was coming from the update method in the toys_controller

    -After examining the code in the controller I realized it was trying to update the param[:id] which was not included in the toy_params method in the private section, the part of the error that said "Unpermitted parameter: :id" made more sense now.

    -After including the [:id] param in the method the likes are updated smoothly



- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    -After trying to donate a toy a routing error appeared on the server logs specifically there were no delete route matches according to the logs so I went to /config/routes.rb to confirm this

![img](https://github.com/moringa-school-labs-and-assignments/phase-4-debugging-network-requests-lab/blob/main/images/Screenshot%20from%202023-06-25%2007-16-27.png?raw=true)

    -So I added a destroy route by using the available resource and confirmed that it was up and running

    
![img](https://github.com/moringa-school-labs-and-assignments/phase-4-debugging-network-requests-lab/blob/main/images/Screenshot%20from%202023-06-25%2007-21-28.png?raw=true)



    -Next, I went to the toys_controller to check if there was an action to the delete route.

    -Now on donating the toy, there were no issues

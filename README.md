I am building a simple Go server which serves the request of the client. Basically I am making three routes that are, “/”, “/hello” and “/form”.
Client can request any of the three path mentioned above and our server will simply handle the requests.

### The flowchart

![image](https://github.com/user-attachments/assets/d266a941-27d9-4664-a9f0-31390f6b779e)


Here, I am creating three files 
1. index.html
2. form.html
3. main.go

Let me explain what is there in these files →

As this project is very simple and I am making it just to understand the concepts of GO, I am keeping the HTML files very simple.

### index.html

In this file I am just writing simple thing on the very simple boilerplate of html, that this is the static website and this URL routes to the index.html file.



### form.html

Here I am creating just a simple form which takes two inputs one for the name and another one for the address. After submiting we will display the inputs on the screen.



### main.go

Here I am writing the code for go which will help me in creating routes for different URLs



Thats it now just run 
`go run main.go` 

And visit port 8080.

:)

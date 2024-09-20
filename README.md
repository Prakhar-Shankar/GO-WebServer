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

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Static Website</title>
</head>
<body>
    <h2>Hii this is a static website and it routes to the URL "/index.html"</h2>
</body>
</html>
```

### form.html

Here I am creating just a simple form which takes two inputs one for the name and another one for the address. After submiting we will display the inputs on the screen.

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form</title>
</head>
<body>
    <div>
        <form method="POST" action="/form">
            <label>Name</label> <input name="name" type="text" value="">
            <label>Address</label> <input name="address" type="text" value="">
            
            <input type="submit" value="submit">
        </form>
    </div>
</body>
</html>
```

### main.go

Here I am writing the code for go which will help me in creating routes for different URLs

```jsx
package main

import(
	"fmt"
	"log"
	"net/http"
)

func formHandler(w http.ResponseWriter, r *http.Request){
	if err := r.ParseForm(); err != nil{
		fmt.Fprintf(w, "ParseForm() err:= %v", err)
		return
	}
	fmt.Fprintf(w, "POST request successful!")
	name := r.FormValue("name")
	address := r.FormValue("address")
	fmt.Fprintf(w, "Name = %s\n", name)
	fmt.Fprintf(w, "Address = %s\n", address)
}

func helloHandler(w http.ResponseWriter, r *http.Request){
	if r.URL.Path != "/hello"{
		http.Error(w, "404 Not Found", http.StatusNotFound)
		return
	}
	if r.Method != "GET"{
		http.Error(w, "Method is not supported", http.StatusNotFound)
		return
	}
	fmt.Fprintf(w, "Hello MadaFaka!!!\n")
}

func main(){
	fileServer := http.FileServer(http.Dir("./static"))
	http.Handle("/", fileServer)
	http.HandleFunc("/form", formHandler)
	http.HandleFunc("/hello", helloHandler)

	fmt.Printf("Starting server at port 8080\n")
	if err:= http.ListenAndServe(":8080", nil); err !=nil{
		log.Fatal(err)
	}

}
```

Thats it now just run 
`go run main.go` 

And visit port 8080.

:)

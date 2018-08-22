---
layout:     post
post_id :   22
title:      How To Scrape A Website That Requires Login With Golang?
date:       2018-08-23 00:10 +0545
author:     "Sandip Bhagat"
---

If you have been following my blog, you know, how much I love `Python`. It has been my goto language for scraping related works. I use Python and Django both at office life and personal life. I can do so much with little code and in so much less time. But recently, there has been a buzz for `Go` or `Golang` [as someone says] which made me to look into it. As a way to practice my knowledge and understanding of `Go`, I thought to write a program to scrape a website that requires login. I usually start my learning of any language from scraping [if possible] because it interests me so much. 

In `Go` however, scrapping wasn't very straight forward as I expected so I decided to write a tutorial for it.

In this tutorial, we will write a Go program to scrape a list of projects from our [Gitlab](https://gitlab.org) account.

The source code for this tutorial can be found on my [Github](https://github.com/sandipbgt/golang-scraper-example)

First visit the following page [https://gitlab.com/users/sign_in](https://gitlab.com/users/sign_in) . You will see the page as below.

![Gitlab signin page]({{ site.url }}/img/posts/2018-08-23-scraping-tutorial-with-golang/1.png)

**Note:** If you are logged in, perform logout first. 

Now in order to login to the site, we need to extract some information from the site and build a `url.Values` struct which is required while posting to a form in `Go`.
Right click on the "Username or email" field and select "inspect element". We will use the value of the name attribute for this input which is `user[login]`. This will be the key in the struct and our username/email will be the value. This may be different depending on the site.

![Gitlab signin page username field]({{ site.url }}/img/posts/2018-08-23-scraping-tutorial-with-golang/2.png)

Right click on the "Password" field and select "inspect element". The value of the name attribute for this input is `user[password]`. This will be the key in the struct and our password will be the value. Again, this may be different depending on the site.

![Gitlab signin page password field]({{ site.url }}/img/posts/2018-08-23-scraping-tutorial-with-golang/3.png)

Another name attribute required is `authenticity_token`. Most of the sites will have this as a hidden input tag. We will use this as key in the struct and its value as well.

![Gitlab signin page authenticity token]({{ site.url }}/img/posts/2018-08-23-scraping-tutorial-with-golang/4.png)

The above instructions differs depending upon the site. While this login form is simple, some sites might require special parameters that we should use for the login step.

Now let's write some `Go` code.
Create a project in our Go workspace:

{% highlight bash %}
mkdir -p $GOPATH/src/github.com/<your github username>/golang-scraper-example
{% endhighlight %}

We will be using `goquery` library so install it by typing:
{% highlight bash %}
go get github.com/PuerkitoBio/goquery
{% endhighlight %}

Next, create a file named `main.go` inside that directory, containing the following Go code.

Create a package `main` and import the required library.

{% highlight bash %}
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
	"net/http/cookiejar"
	"net/url"
	"strings"

	"github.com/PuerkitoBio/goquery"
)
{% endhighlight %}


Create a global constant `baseURL` to store base url of the website and variables `username` and `password` to store gitlab username and password respectively.

{% highlight bash %}
const (
	baseURL = "https://gitlab.com"
)

var (
	username = "your gitlab username"
	password = "your gitlab password"
)
{% endhighlight %}

Create struct `App` to store our `http.Client`, `AuthenticityToken` to store `authenticity_token` value and `Project` to store the list of repositories scraped from gitlab account.

{% highlight bash %}
type App struct {
	Client *http.Client
}

type AuthenticityToken struct {
	Token string
}

type Project struct {
	Name string
}
{% endhighlight %}

Create a receiver function `getToken()`. This function will scrape the value of hidden input `authenticity_token` from gitlab signin page. Without this field, we won't be able to login. Here, first we are doing a get request to the login page and then passing the response body to `goquery` to get a struct document of type `Document`. It represents an HTML document to be manipulated. On this document, we can make selections to get the token using jQuery like syntax. We are storing the value of the token in `AuthenticityToken` struct and returning it.

{% highlight bash %}
func (app *App) getToken() AuthenticityToken {
	loginURL := baseURL + "/users/sign_in"
	client := app.Client

	response, err := client.Get(loginURL)

	if err != nil {
		log.Fatalln("Error fetching response. ", err)
	}

	defer response.Body.Close()

	document, err := goquery.NewDocumentFromReader(response.Body)
	if err != nil {
		log.Fatal("Error loading HTTP response body. ", err)
	}

	token, _ := document.Find("input[name='authenticity_token']").Attr("value")

	authenticityToken := AuthenticityToken{
		Token: token,
	}

	return authenticityToken
}
{% endhighlight %}

Create another receiver function `login()`. This function will login to the website using the credentials `username`, `password` and `authenticity_token`. We are doing a `PostForm` request in order to login. The value of authenticity_token is received from `getToken` function.

{% highlight bash %}
func (app *App) login() {
	client := app.Client

	authenticityToken := app.getToken()

	loginURL := baseURL + "/users/sign_in"

	data := url.Values{
		"authenticity_token": {authenticityToken.Token},
		"user[login]":        {username},
		"user[password]":     {password},
	}

	response, err := client.PostForm(loginURL, data)

	if err != nil {
		log.Fatalln(err)
	}

	defer response.Body.Close()

	_, err = ioutil.ReadAll(response.Body)
	if err != nil {
		log.Fatalln(err)
	}
}
{% endhighlight %}

Next create `getProjects` function. This function will return array of `Project` structs. It will scrape list of projects from dashboard page and build a struct array.

{% highlight bash %}
func (app *App) getProjects() []Project {
	projectsURL := baseURL + "/dashboard/projects"
	client := app.Client

	response, err := client.Get(projectsURL)

	if err != nil {
		log.Fatalln("Error fetching response. ", err)
	}

	defer response.Body.Close()

	document, err := goquery.NewDocumentFromReader(response.Body)
	if err != nil {
		log.Fatal("Error loading HTTP response body. ", err)
	}

	var projects []Project

	document.Find(".project-name").Each(func(i int, s *goquery.Selection) {
		name := strings.TrimSpace(s.Text())
		project := Project{
			Name: name,
		}

		projects = append(projects, project)
	})

	return projects
}
{% endhighlight %}

Finally, our `main()` function will utilize all the above functions. First, we are creating a `cookiejar` to store cookies required while logging into the website. Next we are creating instance of our `App` struct and passing `http.Client` with `cookiejar`. Then we are calling `app.login()` which will do the login and then we are calling `app.getProjects()` which will scrape list of projects and store in `projects` variable and at the end we are looping through the `projects` array and printing our project name to the console.

{% highlight bash %}
func main() {
	jar, _ := cookiejar.New(nil)

	app := App{
		Client: &http.Client{Jar: jar},
	}

	app.login()
	projects := app.getProjects()

	for index, project := range projects {
		fmt.Printf("%d: %s\n", index+1, project.Name)
	}
}
{% endhighlight %}

To run the program, type from inside your project directory and it should print list of projects from your gitlab account.
{% highlight bash %}
go run main.go
{% endhighlight %}

The source code for this tutorial can be found on my [Github](https://github.com/sandipbgt/golang-scraper-example)
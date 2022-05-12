# Qwentes Application
The maximum delivery time is 10 days from receipt of the specifications via email.

Development can be done on GitHub, GitLab or any other portal. Once finished send the repo link via email (the same email that sent these specs).

## Premise

The exercise consists in developing a portal in Angular that has the following pages:
- [login](#login)
- [contact list](#contact-list)
- [contact detail](#contact-detail)
- [post list](#post-list)
- [post detail](#post-detail)

In the repo you can see all the images of the application that will be developed and the texts contained between `[]` must be replaced with the data taken from http calls, it is strongly recommended to use AngularCLI for the project setup.

In case you fail to complete the whole exercise, the thing that is most taken into consideration is the **quality of the code**, not the quantity:
- how it is structured
- stateless / stateful components
- correct division between UI and business logic

There are no restrictions in the use of a state management, it is at your discretion whether to use it and in which case.

All the API of the exercise come from [jsonplaceholder](https://jsonplaceholder.typicode.com/), in any case each page will indicate which is the call to make to get the data but if there are any doubts you can always consult the site that explains very well how it works.

## Login
> Images: [login](https://github.com/qwentes-team/application-interview/blob/main/01%20-%20Login.jpg) / [login invalid](https://github.com/qwentes-team/application-interview/blob/main/02%20-%20Login%20invalid.jpg)

The portal provides a fake login, the required fields for authentication are:
- email - checking that it is a valid email
- password - minimum 4 characters

If the fields are not valid, the button must not be enabled and the input in error must have a red border.
If the fields are valid, set a `token` key in the localStorage with a value of your choice and redirect to the [contact list](#contact-list) page.
After logging in, a *logout* button will always be visible at the bottom right which will delete the `token` in the localStorage and bring the user back to login.

## Contact list
> Images: [contact list](https://github.com/qwentes-team/application-interview/blob/main/03%20-%20Contact%20list.jpg)

Users must be taken via an http call in GET: `https://jsonplaceholder.typicode.com/users`.
Each user must show:
- Full name
- Street
- City
- Initials of the name and surname *(Ex: if the name is Mario Rossi, the initials will be MR)*

When you click on a user you have to go to [contact detail](#contact-detail)

## Contact detail
> Images: [contact detail](https://github.com/qwentes-team/application-interview/blob/main/04%20-%20Contact%20detail.jpg)

The user detail is obtained through an http call in GET: `https://jsonplaceholder.typicode.com/users/{userId}`.
The page must show a form that allows the modification of some user information:
- Name - minimum 6 characters
- email - checking that it is a valid email
- Company Name

The required fields must be validated and must behave like the login in case of an error. The same goes for the form button.
Once the form is valid, the button is enabled and upon click a PATCH call must start: `https://jsonplaceholder.typicode.com/users/{userId}` passing as payload.
```js
{
	name: "<form value>",
	email: "<form value>",
	company: {
		name: "<form value>"
	}
}
```
Obviously the PATCH call will not really change the data since the APIs are only placeholders, the important thing is to send the payload and have a 200 as a response.
Below the form you must see the posts created by the user we are viewing, they can be obtained by making an http call in GET: `https://jsonplaceholder.typicode.com/posts?userId={userId}`
Each post must show:
- Post title
- Post body

Click on the post to go to [post detail](#post-detail)

## Post list
> Images: [post list](https://github.com/qwentes-team/application-interview/blob/main/05%20-%20Post%20list.jpg)

This is a simple list of posts, the data to be displayed is obtained by making an http call in GET: `https://jsonplaceholder.typicode.com/posts`.
Each post must show:
- Post title
- Post body

Click on the post to go to [post detail](#post-detail)

## Post detail
> Images: [post detail](https://github.com/qwentes-team/application-interview/blob/main/06%20-%20Post%20detail.jpg)

The information to be shown in detail is:
- Post title
- Post body

Available via http call in GET: `https://jsonplaceholder.typicode.com/posts/{postId}`

The author of the post with the information shown in the [contact list](#contact-list), available via http call in GET: `https://jsonplaceholder.typicode.com/users/{userId}`

A list of comments, where each comment must show
- Comment name
- Comment body

Available via http call in GET: `https://jsonplaceholder.typicode.com/comments?postId={postId}`

## Plus
> All the things listed below are only improvements, the exercise is considered completed even without the implementation of these points.

- Make the modules lazy (lazy routes) so that you download the module only when you actually need it
- Add the login control within the Route Guards so as to correctly block the user in case he tries to access sections via URL even if he is not logged in
- Using reactive forms

# User Stories

## Routes
### Web Routes
- /home
- /signup
- /login
- /docs
- /support

### API Routes
- POST /user
- GET /user/:id


## Components
- header bar
- bakeshop logo
- bakeshop wordmark
- buttons
	- signup 
	- login
	- logout
	- signup with google account
	- submit
- form with fields
	- name
	- email
	- password
	- submit button

## DB
### Users Table
- id
- email
- pw_hash or oath_id
- first name
- last name
- biz_belongs_to

### Business Info
- id
- business name
- owner_id?
- has many users through buz_id on User



### Roles Tables
- user_id
- bus_id
- role
- unique user, bus 



## Actions
As a new user, I navigate to the bakeshop url and view the home page.
- there is a header
- the bakeshop logo is visible in the top left corner
- Bakeshop App wordmark is visible somewhere on the header

As a new user, I know that I need to sign up first and click the "signup" button.
- signup button (styled as a link)
- clicking the link takes the user to the sign up page
- logo is visible, but since this is a user-action page, no header needed
- form is visible with fields for:
  - name
	- business email
	- password
- buttons visible for signing up with gmail account

I complete and try to submit the form with invalid information
- form fields validate their contents
- submit button is disabled

I correct the information
- fields should remove warning as soon as proper conditions reached

I submit the form with valid information
- submit button is enabled
- requested posted to server
- confirmation email sent to account
	- best practice confirm account button in email, means to enforce it but not on first day
- directed to main app page with valid login token

As a logged in user I view the main app page
- header
  - logo
	- links to docs and support
	- logout button
	- profile button
- the content of this landing page will evolve as feature functionality evolves
- footer?


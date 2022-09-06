# BandFleaMarket ------- A simple 2 sides Marketplace
********************************

## Github and URL
#### Heroku URL: https://band-fleamarket.herokuapp.com/
#### Github: https://github.com/Todd0554/BandFleaMarket
#### Presentation Video: https://www.youtube.com/watch?v=nBtqX4cnlQM
## Description of BandFleaMarket
#### BandFleaMarket is a second hand music instrument two side marketplace based on ROR 6.1.6 and ruby 2.7.5. This app is for the people who want to buy or sell music instruments or other relative music equipment. Customers can both selling and buying products in this app. If users want to sell or buy products in this app, they need to sign in firstly. Here are several main features of this app:
********************************

### Main problems during designing this app
#### 1. What pages/functions the users can visit/use if they sign in or not? 
#### 2. What is the logic and relations between models, especially Cart model?
#### 3. How to seperate selling and buying when a user signed in?
#### About the question 1, this problem can be seen as the problem of authorise. The users' identifications need to be authenticated before visiting some of the pages in this app. Question 2 is related to models (database), which is related to the relations among different data. In addition, there are also some other basic problems like deployment, authentication and so on.  
********************************
### Project management ----Trello
#### I use Trello to do the project management:
![](/docs/Screen%20Shot%202022-07-06%20at%2020.49.01.png)

### User stories
#### 1. As a seller, I want a page to add product, so that I can add the products I wanna sell.
#### 2. As a seller, I want to check all the products I'm selling, so that I can manage them better.
#### 3. As a seller, I want that only I can edit delete the products I'm selling, so that others can't make any changes on my products.
#### 4. As a buyer, I want to see products in different categories, so that It's easy to find the product I want.
#### 5. As a buyer, I want to have a shopping cart, so that I can add the products I'm interested in into the cart.
#### 6. As a buyer, I want to check my ordering history in one pages, so that I can see what I have bought.
#### 7. As a user without log in, I want to see all the products too, so I can decide whether I want to sign up.
********************************
### Main functions

#### 1. Users can sell and buy products in this app.
#### 2. Users can have their own account.
#### 3. Users can have their own cart and they can add the products they like to the cart.
#### 4. Users can check all the products they are selling now in their own shops. 
#### 5. Users can buy the products and check the ordering history. 
********************************
## Techstack
#### 1. Bootstrap: I choose to install bootstrap 5 to the app, so it can't be seen in Gemfile. I use it to establish the navbar for each page   
![](/docs/Screen%20Shot%202022-07-05%20at%2019.53.32.png)
#### and the dropdown menu:
![](/docs/Screen%20Shot%202022-07-05%20at%2019.40.49.png) 
#### 2. skeleton-rails for the form CSS. 
#### 3. font-awesome-rails for directly using icons from font awesome in erb tag. 
```erb
<%= link_to myshop_path, class: "nav-link", style:"color:#32CCCC" do %>
<%= fa_icon "user" %>
<%= "MyShop" %>
```
![](/docs/Screen%20Shot%202022-07-05%20at%2019.46.09.png ) 
#### 4. image_processing and mini_magick for unifying image size. I define a method in product model like this, and then directly use it in views: 
```ruby
class Product < ApplicationRecord
  belongs_to :user
  belongs_to :category
  belongs_to :sort
  has_rich_text :description
  has_one_attached :picture
  has_many :cart_products
  def newsizeimage
    return self.picture.variant(resize: "300x300")
  end
end
```
#### Thus, when users upload images, the size of each images will be reset.
#### 5. Devise for authentication.
#### 6. aws-sdk-s3 (AWS S3): When I develop this app, I use the active storage to save the uploading image. But when I deploy the app to heroku, I decide to use AWS S3 to save the uploading pictures in production side of the app. 

********************************
### Sitemap
![](/docs/sitemap.jpg) 
#### This is a simple sitemap of this app. In order to express the major connection of each page, I didn't show the basic connection between some pages, such as each page can directly link to the root page and all_the_products_page. the name of each page in this sitemap is not the real page name, I just use these name to show what is the function of the page.   
#### On the right side are the websites can be visited before signing in. The pages which show products (no mater in categories, sorts or all) can be visited any time. However, some functions like buying or adding products to cart in these pages only can be used after signed in. For example, when the user signs in, the adding button is like this:
![](/docs/Screen%20Shot%202022-07-05%20at%2019.15.42.png ) 
#### When the user doesn't sign in:
![](/docs/Screen%20Shot%202022-07-05%20at%2019.17.10.png ) 

#### On the left side are the websites that can be visited after signing in. The nav bar will change when a user sign in. 
#### This is the nav bar before signing in:
![](/docs/Screen%20Shot%202022-07-05%20at%2018.55.35.png ) 
#### This is the nav bar after signing in:
![](/docs/Screen%20Shot%202022-07-05%20at%2018.55.13.png ) 
#### So, If users signed in, they can visit Myshop, Mycart and Myorder pages. In addition, I also add a Trolley icon which link to mycart on the right corner of the page showing products. There is an animation when the customer add a product to their cart. 
![](/docs/Screen%20Shot%202022-07-05%20at%2019.05.05.png ) 
********************************

## Wirefram
### Root page
#### This is the wireframes of the root page. On the top is a navbar with the logo. If the user signs in, they will see the button of myshop, mycart, myorder and sign out. If they don't sign in, they only can see the button of sign in and sign up. Under the nav bar there are 4 categories of different products including guitar&bass, pedals, amplifiers and others. The guitar&bass, pedals and amplifiers are dropdown menus, and under each there are are several different sorts of the products. Users can choose any of them to see the products belongs to that sort. The show all button will take the user to see all the products of this app. In the body part, the button of "I'm looking for something" links to the page showing all the products and the button of "I have something to sell" link to the page to add a product to sell. If the users bg  want to sell the products, they need to sign in before. Under these 2 buttons, there are four sessions same as the categories and each session has the button link to the page which shows the products belongs to this category.
![](/docs/rootpages.png) 

### Products pages
#### The wirframes of products pages (including show in different categories or sort and all the products) are same. Every page only show 5 products and users can click "Next page" or "Previous page" button to control the pages. I also put a trolley logo which link to my cart on the right bottom corner. In addition, I set an "add to cart" button for every product. This button only can be shown if this product is not belong to the current user who signed in now, It's not sold and It has not added to cart by the current user yet. 
![](/docs/products.png) 
#### The page of show one product has "buy now" button to directly buy the product. If the product belongs to the current user, this button will change into "You can't buy the product belongs to you."
![](/docs/show%20one%20product.png) 

### Myshop, Mycart and Myorder pages
#### The wireframes of these 3 pages are almost same as products page. For myshop page, I set a button to sell the products, which means users can create the products they want to sell in myshop page. In addtion, there are buttons of show, edit and delete of each product in myshop page. This can help users edit their products.
![](/docs/myshop.png) 
#### In mycart page, I set a button of "remove the product" to help user manage the products. This page also can calculate the total price of the prodcuts in the cart and there is another "Pay together" buttone to pay for them. 
![](/docs/mycart.png) 
#### Myorder page only show the history of the orders and the ordering time. 
![](/docs/myorder.png) 

### Edit and add products page
#### These 2 pages are also very similar. Users can insert the details of the product here.
![](/docs/edit%20and%20add.png) 

### Sign in/up and forget password pages
#### Sign in page:
![](/docs/sign%20in.png)
#### Sign up page:
![](/docs/sign%20up.png)
#### Forgot password page
![](/docs/forget%20password.png)
### Success page
#### This page will show after users buy products. This page only tell the user they successfully pay for the product. 
![](/docs/success.png)
****************************************************************
## MVC
#### The main architecture of a Rails app is MVC which are Model, View and Controller. Model will select the target data from database and then send them back to Controller. The Controller will transfer the data into View and View will give typography and beautification for these data. 

### Database Design (Model)
#### This app use the Postgresql Database. 
#### ERD
#### This is the ERD for the database tables:
![](/docs/ERD.jpg)
#### Users table save the basic information of each user when they sign up. Products table saves the information of the products any user add to their shop. Orders table is used to save the orders. On the other hand, category table saves 4 categories  which categorise the products. Sort is used to refine the category. Thus, users can check the products not only in different categories but also in different sorts. This app use the active storage to save the description and the image for the products when I test the app locally. When the app deploy on Heroku, the aws s3 will be used to store the image from the users. In addition, I use cartproducts table to link the products table, users table and carts table together. The cartproducts means the products added to cart by the current user. And the carts table save the cart information for each user. 
### Description of the relationship  among models
#### A user can have many products and one product belongs to one user.
#### A user can have many orders as a buyer or seller. Each order belongs to one buyer and one user.
#### A user only has one cart and one cart belongs to one user.
#### A product belongs to one sort and one sort can have many products. 
#### A product belongs to one category and one cate gory can have many products.
#### One sort belongs to one category and one category can have many different sorts. When users add new products and set their sort, the category will be set automatically, because I already set the relations between sort and category in seed.rb. 
#### one cart can have many products through cartproducts and the same product only can be added to the same cart one time.


### Controller
#### This app has several controllers to control the data from database to views. 
#### 1. Products controller is used to control the data of products and show the correct data into different views html files of products. There are many functions in products controller including creating products, editing products, showing products, deleting products and placing order for one product. 
#### 2. Cart_products controller is used to control the action of cartproducts table including adding product to cart and removing products from cart. 
#### 3. Cart controller inherit from products controller. Inheritance is a relation between classes. The child class can have the same methods or variables inside of parent class. For example, all the controller in ROR frame inherits ApplicationRecord class. Thus, all the methods in ApplicationRecord also can be used in any controller. In this app cart controller needs to have a method to place multiple orders together which is very similar to place one order in products controller, so some variables from products controller need to be used in cart controller. This is why I set cart controller inherits products controller.
#### 4. Pages controller is used to control the page of mycart and myshop. 
#### 5. Myorder controller is used to control the pages of myorder. 

### Views
#### By using the model relations and controller together, in the myshop page, the products belongs to the current user can be easily shown. Similarly, in the myorder page, the products whose buyer is same as the current user will be shown. In the mycart page, the products which are added to cartproducts and belongs to the cart of the current user will be shown. 

## Deployment and source control
#### This app is deployed by using Heroku and uses Git to do the source control. During the developing process, I use the Heroku pipeline model to deploy the app. 
****************************************************************
## More screenshot
### Rootpage1
![](/docs/Screen%20Shot%202022-07-08%20at%2010.18.29.png)
### Rootpage2
![](/docs/Screen%20Shot%202022-07-08%20at%2010.18.57.png)
### Products page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.19.10.png)
### show one product page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.26.24.png)
### Sign in page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.19.43.png)
### myShop page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.20.13.png)
### myCart page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.20.33.png)
### myOrder page
![](/docs/Screen%20Shot%202022-07-08%20at%2010.20.42.png)



# FoodPath
## Table of Contents
1. [Overview](#Overview)
2. [Product Spec](#Product-Spec)
3. [Wireframes](#Wireframes)
4. [Schema](#Schema)

## Overview
### Description
Helps users recognize an unknown food dish through image recognition and by specifying the ingredients used in the dish. The app will then recommend and redirect users to other websites that contain the recipes for said dish.

### App Evaluation
- **Category:** Food
- **Mobile:** This app would be primarily developed for mobile. Functionality is limited to mobile devices, specifically only for iOS.
- **Story:** Analyzes the unknown food dish specified by user either through taking a picture or by specifying the ingredients. The user can then choose from a list of recommended recipes to said dish.
- **Market:** Any individual could choose to use this app. This app is targeted so that it is user-friendly and is not hard to navigate through.
- **Habit:** This app could be used as often or unoften as the user wanted depending on how interested they are in cooking. This app aims to also increase the user's interest in cooking.
- **Scope:** First we would ensure that the app successfully recognizes the unknown food dish through image recognition and by specifying its ingredients. From there, our app will recommend a few dishes based off the results above, of which will then recommend a list of recipes accordingly. In the future, we are looking to implement more features to enhance the user's experience, such as through daily recommendations of recipes, history tracking etc.

## Product Spec
### 1. User Stories (Required and Optional)
**Required Must-have Stories**
- [ ] User can select from a predefined list of ingredients
- [ ] User can access camera to take a picture of their food
- [ ] User can check to see if the ingredients recognized are required/wanted
- [ ] User can select the from a list of recommended food dishes
- [ ] User can select from a list of recommended recipes
- [ ] User can be redirected to the website of the recipe

**Optional Nice-to-have Stories**
- [ ] User can save recipes for later reference 
- [ ] User can discover different recipes (be recommended different recipes) based on time of day 
- [ ] User can see a list of recent searches
- [ ] User can change the settings of the app (ex: dark mode)

### 2. Screen Archetypes
* Discover Today *(optional)*
    - User can discover various recipes (get recommendations) 
* Stream
    - User can select from a predefined list of ingredients
	- User can access camera to take a picture of their food
	- User can see a list of recent searches *(optional)*
* Camera
	- User can take a picture of their food
* Image Recognition Details
    - User can verify/uncheck the ingredients that were recognized from the image recognition api
* Food Picker 
	- User can select from a list of recommended food dishes
* Details of Recipes 
    - User can select from multiple recommended recipes 
    - User can save their favorite recipes *(optional)*
    - User gets redirected to the website of the recipe	
* Settings *(optional)*
    - User can change the settings of the app	

### 3. Navigation
**Nav Bar:**
*    Back Button
*    Home button
		
**Flow Navigation:**
* Discover Today *(optional)*
&#8594; Stream
* Stream
&#8594; Discover Today *(optional)*
&#8594; Camera
* Camera
&#8594; Stream
&#8594; Image Recognition Details
* Image Recognition Details
&#8594; Stream
&#8594; Food Picker
* Food Picker 
&#8594; Stream
&#8594; Details of Recipes
&#8594; Image Recognition Details
* Details of Recipes
&#8594; Stream
&#8594; Image/Name/bookmarking option *(optional)*
&#8594; Redirect to website
&#8594; Food picker
* Settings *(optional)*
&#8594; Stream

## Wireframes
![](https://i.imgur.com/XIC1GFg.jpg)

### [BONUS] Digital Wireframes & Mockups
![](https://i.imgur.com/uTD3Gyd.jpg)

## Schema
### Models
#### checkIngredients
|Property	|Type		|Description		|
|:----:		|:----:		|:----:			|
|ingredientId	|Integer	|unique identifier for predefined ingredient|
|ingredientName	|String		|name of predefined ingredient|
|isChecked	|Boolean	|boolean value to check if ingredient has been selected (True/False)|

### Networking
#### List of network requests by screen
- Stream
	- (Read/GET) query all predefined ingredients whose name is query string
	- (Update/PUT) update checked value of predefined ingredient (isChecked is True/False)
- Camera
	- (Create/POST) upload an image for image recognition 
- Image Recognition Details
	- (Read/GET) query all recognized ingredients from list of predefined ingredients from uploaded image using image recognition API
	```
	let labeler = Vision.vision().cloudImageLabeler()
 	labeler.process(image) { labels, error in
		guard error == nil, let labels = labels else { return }

		// Task succeeded.
		// ...
 	}
 	for label in labels {
		let labelText = label.text
		let entityId = label.entityID
		let confidence = label.confidence
 	}
	```
	- (Update/PUT) update checked value of predefined ingredient (isChecked is True/False)
- Food Picker
	- (Read/GET) query all selected predefined ingredients
	- (Create/POST) upload either both image and list of selected ingredients or just the list of selected ingredients to food search api 
	- (Read/GET) query all recognized food dishes from food search api
- Details of Recipes
	- (Create/POST) upload name of food dish to recipe search api
	- (Read/GET) query all recipes related to food dish

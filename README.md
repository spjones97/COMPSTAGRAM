In this problem set you will learn how digital image filters work by implementing a few classics, like border, brightness, and saturation, yourself! These same techniques are used in apps like Instagram and Snapchat to change the overall look of an image.

Browser Compatibility Warning: This problem set requires working in the Chrome web browser. Using Edge, Firefox, or Safari will result in a buggy experience if it even works at all.

Points: 100

Digital Colors are traditionally represented with 3 components: red, green, and blue. If you were to hold a magnifying glass up to your laptop's screen, you would likely see each dot, or "pixel", is actually 3 smaller dots whose colors are red, green, and blue.

By varying the intensity of these red, green, and blue dots, from 0% to 100%, your display can output the entire range of colors you see on your screen. All three at 0% is black, all three at 50% is the mid-range gray, all three at 100% is white. Carolina Blue, for example, is 48.2% red, 68.6% green, and 83.1% blue.

In our code, we will represent these percentages with double values between 0.0 and 1.0.

Digital Images, then, are 2D arrays of Colors. The size of the 2D array depends on the quality of the picture. A modern smart phone, like the one in your pocket, captures pictures with anywhere between 4 to 16 million pixels. (Hence "megapixels".) The Image class lets us store and manipulate hundreds of thousands to millions of Color elements in a 2D array!

Digital photo Filters are algorithms that receive an input Image, process each Color "pixel" in it element-by-element, and return an output Image that has been processed. 

In this assignment you will implement a few Filters each with one specific purpose that can be applied in a varying amount. For example, a Border Filter's goal is to draw a colored border around the Image and the border's thickness is a variable amount. Another example is a Brightness Filter whose goal is to brighten or darken an image by some amount.

To ensure you have the latest material, be sure your development environment is shut down, then pull the latest code and start it back up. Run the following commands in the VSCode Integrated Terminal:

1. Visit: http://localhost:3000/close
a. If there is an error about a timeout this is OK and means your development environment is already closed.
2. npm run pull
3. npm run start

The Color class represents a single, digital color made up of three component colors (properties) which are: red, green, and blue. Your filters will manipulate Color objects, so you should read and familiarize yourself with the Color.ts file.

The Image class represents a digital image via a 2D array of Color "pixels". Its 2D array is organized in a row-major order. Your filters will each apply an algorithm to every pixel in the array. You should read and familiarize yourself with the Image.ts file.

The Filter class will be the superclass of your Filter subclasses. An image Filter is an algorithm that processes an Image and modifies it in some way. For example, in any mobile phone image editing software you're likely to encounter brightness, saturation, border, and other image filters. You should read and familiarize yourself with the Filter.ts file.

Your filter subclasses, and an included demo Filter subclass named "InvertFilter", are located in compstagram-filters.ts. This is the file where you will spend most of your time working.

Support Code

The focus of this assignment is practice writing nested for-loops to process a 2D array. As such, we are providing support code that loads an image, add/remove filters, change the amount each filter is applied, and save photos. If you are curious how any aspect of the app works, feel free to dig into the code in the support folder. You should not need to change any of it to complete this problem set. If you do want to tinker, our recommendation is to wait until you've submitted for full credit.

Image and Color data. The user interface for interacting with your filters is provided in support code. From it you can:

1) Load a different image than the default Old Well image. (You're also free to change the default image if you'd like to!)

2) Select the filter(s) you are applying to the image.

3) Manipulate the amount the filter is applied from 0.0 to 1.0. This value will be given to your Filter. Our code will then run your Filter and display the results.

4) Save your Image after your Filter has been applied for Twitter/Instagram glory.

## 2.0 Invert Filter (Freebie)
If you run the app you'll notice only the InvertFilter is enabled. This is intentional! Try pressing the add button to add the InvertFilter to the app and click the amount slider around with your mouse. (Reminder: only Google Chrome is supported in this problem set. Be sure you are using Google Chrome!)

The class InvertFilter is given to you in its entirety with narrative code comments. This is meant to serve as an example for how a Filter class is structured and how a processing algorithm is implemented. You should read InvertFilter for understanding and tinker around with its amount slider in the GUI before writing your own.

## 2.1 Border Filter
The first Filter for you to implement is BorderFilter. To get started, in compstagram-script.ts, find the TODO comment and uncomment the line where the BorderFilter class is added to model's filterClasses array property. Try running and you should see "Border" show up in your Filter drop-down now. If you try changing the "Amount" slider, nothing happens! Your work begins...

Find the BorderFilter class in compstagram-filters.ts. The goal of BorderFilter is to add a border around your input Image whose borderthickness is controlled using the amount property. The app's amount slider will set this value between 0.0 (meaning no border) and 1.0 (meaning entirely border).

You'll use the following formula for calculating the border's width:

borderthickness = imagewidth / 2 * filteramount 

You'll need to setup a local variable within the process method to hold borderthickness. Its type will need to be a number, however it will need to store only whole numbers because the thickness refers to indices in the 2D array of pixels. You will need to use the floor of your thickness expression above:

let thickness: number = Math.floor( <expression> );
Spend a minute to reason through why you're using this formula. Why are you dividing the image's width in 2? What is the impact of multiplying half of the width by a value between 0.0 and 1.0?

In the same way that InvertFilter's process method works, you'll need to:

1. Create a local variable to hold a copy of the input Image 

2. Write a nested for loop to iterate through and process every pixel

3. Return the copy Image

Now that you know the border's thickness and you're iterating through every pixel in the Image, how will you know whether any individual pixel is a part of the border or not? Using the row and column of a pixel, if any of the following four inequalities are true, you'll know you are in a border area:

Left	col < borderthickness
Right	col >= imagewidth - borderthickness
Top	row < borderthickness
Bottom	row >= imageheight - borderthickness
If you are in a border area, the Color you will set each border pixel to is held in this BorderFilter's property named color.

It's a good idea to start with trying to draw one of the border sides first and then add the others one-by-one. Drawing a border will put your knowledge of if-else-if statements and boolean logic to good use!

## 2.2 Brightness Filter
Let's make it possible to add lightness or darkness to your Images!

Now that you've been around the block with the Border filter, you'll take on modifying pixels by their red, green, and blue component values. Move on to the BrightnessFilter class in compstagram-filters.ts. Notice it has a lot of similarities with BorderFilter. Again, you're tasked with implementing the process method's algorithm.

Be sure to uncomment the BrightnessFilter class from compstagram-script.ts. This will cause the Brightness filter to show up in the filter select menu.

For Brightness, and the filters that follow, we will not walk through the steps to copy the input image, process it via for loops, and return the processed image. Refer to those steps from BorderFilter or InvertFilter.

With BrightnessFilter, you want an amount of 0.5 to result in no change in brightness to your image, 0.0 to be 100% darker than the input, and 1.0 to be 100% lighter than input. Remember, as each red/green/blue component of a Color decreases toward 0.0 it becomes darker. As each increases toward 1.0 it becomes lighter.

As such, here is a formula for calculating our brightness factor.

factorbrightness = (filteramount - 0.5) * 2.0

Take a minute to think about what your brightness factor will be if your filter's amount is any of 0.0, 0.5, and 1.0. Essentially, you're "translating" amount to between -0.5 and 0.5 and then "scaling" it by 2.0 so that your possible factor domain is between -1.0 and 1.0.

Now that you have that stored in a local variable, you need to manipulate each of pixel's three components (the red, green, and blue properties) with the following formula:

outputcomponent = inputcomponent + ( factorbrightness * inputcomponent )

To modify each pixel's components, you'll first need to access the Color pixel from your copy image's pixels array, then manipulate each of its component values. For an example of working with components like this, refer to InvertFilter's process method.

## 2.3 Colorize Filter
Let's make it possible to bring your Image's Colors closer and closer to Carolina Blue (or any other Color)!

Phew, two Filters under your belt. Nice work! Now that you've got Border and Brightness down, you're going to write an algorithm to bring an input Color closer and closer to being another Color. You'll do this for every Color in your Image.

If you think about this in terms of an input Color of white, with RGB components of (1,1,1), and a target Color of black, with RGB components of (0,0,0), you can say you've brought our input 50% closer to your target if its new RGB components are (0.5, 0.5, 0.5). In essence, you've subtracted half of the "distance" between your input color and your target color.

ColorizeFilter's amount property will control the delta, or the percent of the "distance" you'll move each Color from its input toward its target (i.e. Carolina Blue). So an amount of 0.0 will be no change, 0.5 is 50% closer to Carolina Blue, and 1.0 is turning each Color completely Carolina Blue. Here's how you can calculate the delta for any component.

deltacomponent = ( targetcomponent - inputcomponent ) * filteramount

Your target Color is held in this ColorizeFilter's color property, just like with BorderFilter.

Now that you have your delta for each component, add it from the respective input component and apply it to the pixel you're processing, as below.

outputcomponent = inputcomponent + deltacomponent

The InvertFilter goes through a very similar process and may help illustrate what's going on. In InvertFilter, though, each pixel's target color is that color inverted. Here it's the Color stored in the color property.

## 2.4 Contrast Filter
Contrast is the difference in color that makes features of an image perceptible. This is a hard to explain in with words but the filter is easy to see when looking at example pictures or by playing with contrast of a photo on your phone.

In essence, as you reduce the contrast of an Image, you are pulling each of its Colors closer and closer to 50% gray (0.5, 0.5, 0.5). It turns out you've already done this with our Colorize filter! There's an extra wrinkle, though: how do you increase contrast? What does it even mean to increase contrast? If you think of increasing as the opposite of decreasing it would follow you're pushing a Color further and further away from 50% gray.

You'll achieve increasing and decreasing contrast by combining the techniques you applied separately in brightness and colorize.

In BrightnessFilter, you apply some arithmetic to amount to come up with a factor whose domain is between -1.0 and 1.0. With Contrast we'll do something similar except flip the signs by subtracting from 0.5. The rationale for this is as you decrease contrast you want to move closer to gray.

factorcontrast = (0.5 - filteramount) * 2.0

In ColorizeFilter, you have an algorithm for bringing each Color in an Image some amount closer to a target color. In ContrastFilter you will need to use factor instead of amount when finding the delta. Spend a minute reasoning through what impact this should have on varying component values.

deltacomponent = ( targetcomponent  - inputcomponent ) * factor

Otherwise, your contrast algorithm is the same as colorize's assuming your target color is 50% gray or new Color(0.5, 0.5, 0.5).

## 2.5 Saturation Filter
Your last required filter! Good news: it's really easy after doing contrast! Our SaturationFilter is the exact same as ContrastFilter, with one minor tweak: your target Color is different for each pixel. Let's back up.

You can think of Saturation as the intensity of non-gray Colors in an Image. A completely desaturated Image can be thought of as a grayscale or "black and white" Image. Black and white photos are actually many shades of gray. An interesting property of pure black, grays, and white is that each of their three component values are exactly the same. White is (1, 1, 1), grays vary from (0.99.., 0.99.., 0.99..) to (0.5, 0.5, 0.5) to (0.01,0.01,0.01) and black is (0,0,0). Grayscale implies the red, green, and blue components of each Color are equal to one another.

How can you convert any Color to be grayscale? Spend a minute to think about this.

It turns out there are many ways to convert a non-gray Color to grayscale. (You can read a lot on the internet about it!) For this assignment, you'll use a simple hack: take the average of each component and use that.

componentaverage = ( componentred+ componentgreen + componentblue ) / 3.0

You'll construct a new Color using that average value for each of its red, green, and blue components. This will be your target grayscale Color.

Each pixel you process, then, has a different target Color. Barring this difference, the algorithm to implement in SaturationFilter is exactly the same as ContrastFilter. We'll leave this one to you to modify the work you did in Contrast!

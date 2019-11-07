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

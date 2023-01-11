WHY NOT A GIF HERE? TO SET THE MODE.

# Gooh-Gooh Island

The Gooh-Gooh Island is nicely located in the Yrgopelago.

# Hotel Yahoo

The Yahoo Hotel is the one and only on Gooh-Gooh Island. Our slogan is "There is Yahoo".

# Instructions

FYI (For Your Information): our website http://jonas128.se/hotel/

# Code review

1.   hotelFunctions.php: 7 - The checkRoomAvailabilty function uses the connect() function but still receives $hotelDb already connected as an argument. This makes the code harder to understand and maintain. 

2. booking.php: 11-13 - These POST variables should all be sanitized. Even if your form only accepts numbers someone could easily send a POST request containing malicious code with Postmaster, Guzzle or just by editing your form in the inspector.

3. booking.php: 17 - Variable should be in plural, i.e $totalFeatures

4. booking.php: 18 - Even if this works for the prices you want to set, this kind of structure makes it difficult to change your prices without changing your code structure first. It also creates a potential security vulnerability since someone sending a post request with POST[“room”] = -3 or less would have a cost of 0 or less.

5. booking.php: 30 - Rather than divide by 86400 I would prefer (60*60*24) to make it a bit clearer what the number means.

6. booking.php: General - There is a lack of checks and validations. For example, the code never checks if arrival_date is set before departure_date, which means you can book a negative amount of nights and get rooms for negative cost while messing up your database.

7. booking.php: 62 - This comment is incorrect, and might confuse a reader. The code will continue to run even if $roomAvailable = false and the code has done no other checks or validations.

8. booking.php: 79-112 - This nested if structure is a bit hard to follow. Connecting the else statements with the correct if-statement isn’t as intuitive as it could be. I would have preferred resolving the errors first, i.e: 
if(count($roomAvailable != 0){
	echo “error”
}else if(!$validUUID){
	echo “error”
}else{
	“code”
}

9. bookFunctions.php 15-19 - Since :departure_date should always > :arrival_date for a particular booking the code can be simplified. "$arrivalDate < :departureDate & departureDate > :arrivalDate" Does the same thing as your code but is much easier to read. 

10. bookFunctions.php: 35-75 - $response[“error”] will still be empty if Guzzle cannot connect to the server. So you should be using catch-try to check for connection errors. 

I also think you should be using the error messages rather than just returning false. Especially when checking the transfer code it would be nice to tell the user why their code was rejected.

11. script.js: general - There are no comments and a somewhat unclear structure. It is kind of hard to see what belongs together and what doesn’t, and the purpose of some parts are hard to discern. Structuring it into clear sections would help a lot.


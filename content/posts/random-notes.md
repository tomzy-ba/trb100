+++
title = 'Random Notes'
date = 2024-01-31T20:10:55Z
draft = true
+++

## Basic Javascript
- .replace can be used to remove parts of a string


1. Pass Fred into the hash function to get the hash code 385
2. Find the bucket at index 385
3. Store the key value pair in that bucket. eg. Key: Fred, value: Smith



- The String() function can be used to turn a variable/boolean into a string
- Includes() can be used to check if variable contains something
	- you can use if ("aeiou".includes(letter)) to check if a letter is a vowel.
- .sort() is used to sort an array, .sort((a, b) => a -b) sorts in numerical order
- .replace can be used to remove things from an string like .replace(/!/g, "") would remove all "!" from a string. (this is using regex)
	- you can put a function in .replace like: return dna.replace(/[ATCG]/g, (match) => {
- if (number % 2 === 0) is the way to check if a number is even 
- .slice() can be used to remove parts of a string 
- .split can be used to seperate a string into an array, however you cannot use it on a number.    .split(" ") can be used to split the array where the spaces are
- .map can be used to convert each digit string into a number, basically parseInt for an array.
- x ** 2 can be used to square a number
- toUpperCase() can be used to convert a string to capitals

- regex is the best way to filter strings, 
  return /^(\d{4}|\d{6})$/.test(pin); 




[Links?](#)
[Embbed Videos?](#)
<iframe width="560" height="315" src="https://www.youtube.com/embed/tcUDwkvAs-Y?si=bBXgCE3jewDL8KPG" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
# Summary

----
# Related Stuff
[[Dart Factory Constructors]]
#javascript 

----
# Notes:
- This video goes over lessons learned while sound slice was being built.
- It introduces a bunch of cool techniques and stuff.
- Optimization techniques:
	- profiling with dev tools
	- understanding garbage collector and how it affects program performance.
		- minimize the number of times the garbage collector cleans stuff up
		- have factory functions that populate stuff
	- caching
		- factories (design pattern)
			- factories represent instantiated values you should instantiate again in order to save up on memory cost.
		- singletons (design pattern)
	- bitfields 
		- in javascript, booleans take 8 bytes. 
		- you only need 1 bit for a boolean.
		- use a number as a bitfield and cache it. Modify the bit locations when saying true or false. The bit locations represent your boolean. 
			- in your application code, you will have to handle that the bit locations are correct and you modify them correctly. You can create an api to do this. 
## Questions:

## Follow Up:

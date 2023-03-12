<iframe width="560" height="315" src="https://www.youtube.com/embed/MbslvX0AMVE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary:
# Related Stuff:
[[Authentication - Go Web Intermediate Udemy Course]]
[[Authentication - Building Web Applications With Go - Intermediate - Udemy]]
#golang 
#webapplications 
#nodejs 
# Notes:
- Pagination uses offsets and limits. The offset is how far from the beginning of our results. Max limit is the limit of items we want to display per page. For example, say we have a max limit of 20 items and a offset of 0. That means we are going to have the first 20 items. In order to get the next batch of 20 items, the limit will remain 20 and our offset will be 20 ;)
- Filtering limits load on our db by performing a search 
- Filtering limits load on our db by performing a search and we return items that match our filter query parameter. 
	- I do want to see if there are two kinds of filtering: client side and server side.
	- Server side filtering sounds like it covers the case where we search against the db and return specific items.
	- If client side filtering is a thing, it would be filtering the results we get back from the server within the browser and we won't hit the db.
- Pagination is always the default for websites that have a large database (ecommerce applications, for example). Filtering is optional.
	- They mentioned something about a vulnerability for filtering which can lead to DDOS. I wonder what can be done to prevent that exploitation.
- For the Pagination, she also mentioned that we can borrow (or maybe utilize)  concepts from Hypermedia. Pretty much, provided links/url's we can use to get the next page or previous page.
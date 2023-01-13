# Summary:
- Coupling can make it difficult to refactor our database if we have a multiapplication database environment.
- To make our lives easier for database refactoring, we need to encapsulate access to the database and that can be done with a persistance layer.
# Related Stuff:
[[A humble point of view on how to organize persistence in Go]]

#golang 
#databases

# Notes:
- Coupling between a single application and database is easy to maintain and easier to refactor.
- <mark style="background: #FFB86CA6;">Coupling</mark> with multi-application database makes it more difficult to refactor.
- To improve the odds that we can refactor, we need to <mark style="background: #FFB86CA6;">decrease the coupling</mark>. And we can do that by <mark style="background: #FFB86CA6;">encapsulating access to the database</mark>. By that, it means we abstract away the implementation details and define an interface that can be used by applications (an api to access the database). This means we don't have the lower level details or queries directly in our busines logic. 
-  A persistence layer can be implemented in several ways—via data access objects (DAOs), which implement the necessary SQL code; by frameworks; via stored procedures; or even via Web services
- You can never get the coupling down to zero, but you can definitely reduce it to something manageable.
- Database Access Object:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9fVQ_mvzV48" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
- Stored Procedure:
  <iframe width="560" height="315" src="https://www.youtube.com/embed/NrBJmtD0kEw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

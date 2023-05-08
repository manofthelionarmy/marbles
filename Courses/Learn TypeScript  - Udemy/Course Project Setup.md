[Links?](#)
[Embbed Videos?](#)
# Summary

----
# Related Stuff

----
# Notes:
- To transpile (or compile?) typescript into javascript, we need a tool. Microsoft has a tool called tsc, which we install via:
```bash
npm install -g typescript
```
- What is lite-server?
	- https://www.npmjs.com/package/lite-server
> Lightweight _development only_ node <mark style="background: #FFB86CA6;">server</mark> that serves a web app, opens it in the <mark style="background: #FFB86CA6;">browser</mark>, <mark style="background: #FFB86CA6;">refreshes</mark> when html or javascript change, <mark style="background: #FFB86CA6;">injects CSS changes</mark> using sockets, and has a fallback page when a route is not found. 
- it sounds like lite-server is a development server we can spin up locally that has hot reloading capabilities for html and javascript changes, as well as picking up changes to css via sockets.
	- really neat, I should use this for my 50 html,css, javascript projects
- Wait a sec, this project hasn't been maintained for years, and it looks like there's a high vulnerability. Will it be safe to run this locally or should I use vite?
- I think I'll use vite, it has `vanilla-ts` as a preset.
- I do want it setup in Vite to where we throw type checking errors, however, I found out Vite transpiles only (meaning it will treat type check errors as silent errors).
	  - [Vite Transpiles Only](https://vitejs.dev/guide/features.html#typescript)
- The documentation does suggest some things to do to catch the type check errors.
- One suggestion is to the use the [vite-plugin-checker](https://github.com/fi3ework/vite-plugin-checker)
- Here's the guide in how to set it up:
  [Getting Started - vite-plugin-checker](https://vite-plugin-checker.netlify.app/introduction/getting-started.html)
```bash
npm i vite-plugin-checker -D
```
## Questions:

## Follow Up:

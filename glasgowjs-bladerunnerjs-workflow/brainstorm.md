- intro
- brjs
- what is a workflow/
 - build stuff
 - well thats:
   - concatenation 
   - minification
   - dependencies
   - linting
   - less/sass compilation
   - add version number (cache buster)
   - app cache
   - testing
 - that takes time
  - particulary if we have to run the command every time
  - watching a dir can be slow if we produce new files every time
  
- setup cost of new project
 - making tools work together
 - yoeman helps some way
 
- tools dont understand dependency analysis
 - only concatenate what i actually use

- different dev/prod apps/environments


- brjs workflow
 - `brjs serve`
 - open browser
 - write code/css
 - refresh
 - rinse and repeat
 
- testing

- single person workflow is great, now try to scale and parrallelise
 - stuff breaks
 
- blades - seperate working areas/slices of functionality



- no build file


- so how does BRJS help?
- first, what is BRJS
 - bundlers
 - testing
 - java, not node.js
 - deploy wars or flat files*
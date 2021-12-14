## The Golden Rule: 

🦸 🦸‍♂️ `Stop starting and start finishing.` 🏁

If you work on more than one feature at a time, you are guaranteed to multiply your bugs and your anxiety.

## Making a plan

1) **Make a drawing of your app. Simple "wireframes"**
1) **Once you have a drawing, name the HTML elements you'll need to realize your vision**
1) **For each HTML element ask: Why do I need this? (i.e., "we need div to display the results in")** 
1) **Once we know _why_ we need each element, think about how to implement the "Why" as a "How" (i.e., `resultsEl.textContent = newResults`)**
1) **Find all the 'events' (user clicks, form submit, on load etc) in your app. Ask one by one, "What happens when" for each of these events. Does any state change?**
1) **Think about how to validate each of your features according to a Definition of Done. (Hint: console.log usually helps here.)**
1) **Consider what features _depend_ on what other features. Use this dependency logic to figure out what order to complete tasks.**

Additional considerations:
- Ask: which of your HTML elements need to be hard coded, and which need to be dynamically generated?
- Consider your data model. 
  - What kinds of objects (i.e., Dogs, Friends, Todos, etc) will you need? 
  - What are the key/value pairs? 
  - What arrays might you need? 
  - What needs to live in a persistence layer?
- Is there some state we need to initialize?
- Ask: should any of this work be abstracted into functions? (i.e., is the work complicated? can it be resused?)


## HTML SETUP

### Home page/list page
- Div to hold list of plants
    - each plant should be a link to its detail page (anchor tag) (in render function wrap it in `<a>` tag and set href to have id query string in the URL)

## EVENTS - Home
- on load
    - gets plants from the database
        - use async and await - to call a function that calls the server and returns the array of plants
    - displays those plants (loop, render, append)
        - for loop
        - call render function that returns DOM node of each plant
        - append to list container

### Detail page
- Div to hold specific plant details

## EVENTS - details page
- on load
    - figures out which plant object to fetch based on URL query string
    - fetch the specific plant object from the database\
    - display this single plant info
        - call render function to return DOM node of all plants details
        - append DOM node to details container

## FUNCTIONS

### fetchPlantsArray()
  - in seperate fetch-utils js
  - remember: have supabase URL + Key with: const client = supabase.createClient(URL, Key)
  - remember: add supabase CDN script tag to head of HTML file
  - remember: export async function fetchPlants()
  - remember: await keyword
  - const returnedStuff = await client
    - .from('name of table')
    - .select();
- return the data you want from the returned object  
    - return returnedStuff.data

### fetchPlantObject(id)
    - use URLSearchParams to grab the ID of the desired object from the URL. hint: new URLSearchParams(window.location.search), then use .get('id')
    - then you have the id
    - use async/await function
    - const returnedStuff = await client
        hint: .from('name of table) .select() .match({id:id}) .single();
    return returnedStuff.data
    



### renderListOfPlants
    - creates DOM elements
    - sets textContent and other properties equal to data in object
    - remember: set href of anchor tag to './detail/?=${id}' using query string
    - add classlists
    - appends in Div
    - returns DOM node

### renderDetailOfPlant
    - create DOM elements
    - sets textContent and other properties
    - add classLists
    - append in Div
    - return DOM node
Imgur Favorites Cleaner Bookmarklet
===================================

This JavaScript bookmarklet checks if the current page is an Imgur URL, collects links to specific Imgur favorites, displays these links in a new window, and removes them from the favorites if available.

Usage
-----

1.  **Copy the bookmarklet code** provided above in one-liner bookmarklet form, changing YOURUSERNAME to ... your username.
2.  **Create a new bookmark** in your browser, and paste the code into the URL field.
3.  **Name the bookmark** to make it easily identifiable, such as "Imgur Favorites Cleaner."
4.  Navigate to Imgur and log in to view your favorite images.
5.  **Click the bookmarklet** while on an Imgur page to execute it.

What It Does
------------

1.  **Verifies the Domain:** Only runs if the current page’s domain is Imgur.com.
2.  **Finds Favorite Links:** Scans the page for links to your favorites (specifically `/user/mollyrealized/favorites`), and collects the base URLs for each favorite.
3.  **Displays Links:** Opens a new browser window to display the list of collected links in a readable format.
4.  **Removes Favorites:** If favorites are displayed on the page, it automatically removes them by simulating clicks on the delete button for each favorite.

Bookmarklet Code
----------------

```javascript
(function(){
    if(!location.hostname.includes('imgur.com'))return;
    const links=Array.from(document.getElementsByTagName('a'))
        .filter(l=>l.href.endsWith('#/user/YOURUSERNAME/favorites'))
        .map(l=>l.href.slice(0,-'#/user/YOURUSERNAME/favorites'.length))
        .join('\n');
    try{
        const w=window.open();
        if(!w)return;
        w.document.write(`<pre style="word-wrap:break-word;white-space:pre-wrap">${links}</pre>`);
        if(w.document.body.innerText===links)
            Array.from(document.querySelectorAll('.FavoritesPostDelete')).forEach(x=>x.click());
    }catch(e){}
})();
```

Important Notes
---------------

*   This bookmarklet is intended for use only on Imgur pages where you have favorites.
*   Ensure that you’re logged into your Imgur account before running this bookmarklet.
*   Bookmarklet functions may vary based on Imgur’s page structure and may require updates if Imgur changes its site layout.

* * *

This README covers the bookmarklet’s functionality, setup, and important considerations when using it.

# Creating a Bare Bones OPAC

In week 10, we created a Bare Bones OPAC.  This included creating an HTML Form and a PHP Search Script.

## HTML

The HTML form contains the search input boxes.  See code sample below:

```
    <h2>My Basic Library OPAC</h2>

    <form method="post" action="search.php">
        <label for="search">Search Terms (optional):</label>
        <input type="text" name="search" id="search">
        
        <br>
        
        <label for="start_date">Start Date:</label>
        <input type="date" name="start_date" id="start_date" required>
        
        <br>
        
        <label for="end_date">End Date:</label>
        <input type="date" name="end_date" id="end_date" required>
        
        <br>
        
        <input type="submit" value="Search">
    </form>
```

## PHP Search Script

The PHP search script contains the search logic.  It is called from the HTML form in the form method - `<form method="post" action="search.php">`.

The PHP search script builds a SQL statement based on the values entered on the HTML form and returns the results in a grid of columns and rows.  

## More Information

See the [Creating a Bare Bones OPAC](https://cseanburns.github.io/systems-librarianship/5b-basic-opac.html) lecture text to view the sample HTML Form and PHP search script.  

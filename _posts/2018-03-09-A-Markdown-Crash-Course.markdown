---
layout: post
title:  "A Markdown Crash-Course"
date:   2018-03-01 13:10:36 +0100
categories: misc
permalink: "/A-Markdown-Crash-Course"
---

Markdown-syntax has already crossed my path both when producing reproducible reports using Jupyter and R Markdown notebooks.

To check it's features a bit more comprehensively I decided to make an exercise out of it and go through a detailed blog-post that I found on [ghost.org](https://ghost.org/de/). The article is called [How to Write Faster, Better & Longer: The Ultimate Guide to Markdown](https://blog.ghost.org/markdown/). Below will find all the snippets that I tried out myself while going through their article:

The *quick* brown fox, jumped **over** the lazy [dog](https://en.wikipedia.org/wiki/Dog).

Porchetta short loin chicken shoulder pork belly swine. Ground round biltong alcatra sausage pastrami kielbasa tenderloin filet mignon frankfurter capicola leberkas beef pig pork belly. Flank pork prosciutto sausage shankle shoulder swine burgdoggen drumstick. Turkey leberkas pancetta meatball porchetta ribeye buffalo sausage corned beef cupim meatloaf. Shoulder picanha burgdoggen spare ribs, kevin pastrami alcatra jowl kielbasa ground round turkey hamburger ribeye andouille tenderloin. Jerky rump kielbasa, pastrami tri-tip salami tenderloin short ribs meatloaf turducken beef ribs tail jowl.

---

# Basic Markdown Formatting

Here are the elements we'll use most often:
## Headings

# Heading 1
## Heading 2
### Heading 3
#### Heading 4

## Text
*italic*
**bold**
***bold-italic***
[link](http://www.orf.at)

## Images
![m'lady](http://via.placeholder.com/350x150)

## Unordered Lists
* Milk
* Bread
    * Wholegrain
* Butter

## Ordered Lists
1. Tidy the kitchen
2. Prepare ingredients
3. Cook delicious things

## Quotes
> To be or not to be, that is the question.

---

# Intermediate Markdown Formatting
## Horizontal Rules
---

## Code Snippets
Some text with an inline `code` snippet.

Indenting by **4 spaces** will turn an entire paragraph into a code-block (further down we will learn how to specify the language for a proper syntax-highlighing:

    .my-link {
        text-decoration: underline;
    }

## Reference Lists & Titles
**The quick brown [fox][1], jumped over the lazy [dog][2].**

[1]: https://en.wikipedia.org/wiki/Fox "Wikipedia: Fox"
[2]: https://en.wikipedia.org/wiki/Dog "Wikipedia: Dog"

Anywhere we use a URL, we can follow it with a `"title in quotation marks"` to generate a title attribute.

[Dog](https://en.wikipedia.org/wiki/Dog "Wikipedia: Dog")

## Escaping
\*literally\*

Escaping Markdown characters with a back-slash `\` allows us to use any characters which might be getting accidentally converted into HTML.

## Embedding HTML
<button class="button-save large"> Big Fat Button </button>

Possibly the coolest feature of Markdown is that it also just supports plain old HTML.

So we can drop in any HTML, sharing button JavaScript snipped or iFrame we like and it will work on the page just as normal.

---

# Advanced Markdown
Every example so far has been vanilla, normal Markdown. Those code snippets will work absolutely anywhere which supports Markdown syntax.

Now we are going to look at some syntax which is **not standard** to native Markdown (i.e., they are extensions of the language).

## Strike-throughs (we have to use the html-way of doing it here)
<s>deleted words</s>

## Highlights (we have to use the html-way of doing it here)
<mark>ooooh fancy</mark>

## Automatic Links (works)
https://ghost.org

## Markdown Footnotes (works)
The quick brown fox[^1] jumped over the lazy dog[^2].

[^1]: Foxes are red
[^2]: Dogs are usually not red

## Syntax Highlighting
{% highlight python %}
import sqlite3

class Database:

    def __init__(self, db):
        self.conn = sqlite3.connect(db)
        self.cur=self.conn.cursor()
        self.cur.execute("CREATE TABLE IF NOT EXISTS book (id INTEGER PRIMARY KEY, title text, author text, year integer, isbn integer)")
        self.conn.commit()
        # conn.close()
{% endhighlight %}

Another example using JavaScript Code:
{% highlight javascript %}

// This .js-document is part of the udemy-class called "The Complete Web-Developer Bootcamp".
console.log("PRINT ALL NUMBERS BETWEEN -10 AND 19");
var num = -10;
while(num < 20){
    console.log(num);
    num++;
}
{% endhighlight %}

# Converting HTML to Markdown
A [very handy tool](https://domchristie.github.io/turndown/) comes from Dom Christie which easily allows you to convert HTML to Markdown.

# Best Markdown Apps
Writing in Markdown also easily allows you to export to HTML, PDF, or a wide variety of document types.

Some of the coolest Markdown editors for Mac, PC, desktop and mobile are:
## Mac OSX Markdown Editors
* Mou
* iA Writer
* Desk
* ByWord
* SublimeText

## Windows PC Markdown Editors
* WriteMonkey
* MarkdownPad
* Texts
* SublimeText

## Apple iOS Markdown Apps
* Werdsmith
* iA Writer
* ByWord

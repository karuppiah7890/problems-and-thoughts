# Rich Text Format View and Storage

Actually, here, I'm not exactly referring to the Rich Text Format (RTF) extension,
but instead, a general set of problems where rich text needs to be stored. More
like, they are text along with some extra information. This information could
be like font of the text, things like bold/italic/underlined/strikethrough and
so on. This could be text in an ebook, and you might wanna annotate the text,
like a line, with some notes about the line, and also highlight the line. This
text could be part of a social media post or comments or statuses, where certain
words are special words - tags/mentions/hashtags which are part of the text and
start with some special character like "@" or "#" and have a link to it. More
like a hyperlinked text. If you notice, all of this is - adding extra
information to the text. Some example you can think of is HTML, Markdown, where
rich text is shown, with features similar to the above. Now. What if you are
the developer who's trying to developing a rich text editor, more like a
What You See Is What You Get (WYSIWYG) editor, how would you do it? How would
you manage the storage of the content, which has so many properties other than
just a normal string - text - a set of characters. And what if you are building
a comment box for comments in a social media platform, how would you build
the feature to tag people when @ character is typed? How would you store extra
information about the people who are mentioned along with the text? How would you
show the view when the user is typing? The view of the comment box while editing.
Does it highlight the mentioned users? How would you do that? How would you show
it in the view after the post is commented? 

We are talking about efficiently storing and viewing rich text. It would be cool
to know how WYSIWYG editors do it. In the case of HTML, Markdown, there are
parsers to parse the special text that we write. There, the input is different
from the view. Is it possible to give input and have that same input be shown
in the view? Like WYSIWYG editors. Similar to what slack recently introduced.
Some of them hated it. I also get confused with it sometimes. But I wonder how
they built it

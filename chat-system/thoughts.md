If I think about it, in WhatsApp and similar Chat Apps, the central system can
stop storing the messages of users if the message has been sent to all the
users/receivers of the message. Then it's upto the user to make sure that they
don't lose the messages - through local or cloud backups. 

The only problem is, what happens when some of the people from the receivers
list don't come online for a long time? The server needs to keep that user's
messages in it's storage for a long time till those people come online. May be
the server can put such messages in some archive or something and not have it
in its cache? Idk what caching mechanism needs to be followed actually.
Idk if it's even pull based or push based - for getting messages from server.

Need to check how systems like signal app or wire app works.

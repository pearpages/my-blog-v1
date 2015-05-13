Express scaffolding utility
handlebars
html5 boilerplate
Ayi‐ ma’s Redirect Path
middleware

#In express the order in which routes and middleware are added is significant.

Express can distinguish between the 404 and 500 handlers by the number of arguments their callback functions take. 

Express handles the urls in comparison to nodejs.

#Views can use different engines
.jade
.handlebars (based on the popular language-independent templating language Mustache)
express3-handlebars package

#best practices
The first time you do something correctly, it may take five times as long to do it as it would have to do it quick and dirty. The second time, though, it’s only going to take three times as long. By the time you’ve done it correctly a dozen times, you’ll be doing it almost as fast as the quick and dirty way.

.documentation
.attribution
.experimentation

Git, I recommend Jon Loeliger’s excellent Version Control with Git (O’Reilly). 

#Qualit Assurance
.reach
.functionality
.usability
.aesthetics

##Testing
.page testing
.cross-page testing
.logic testing
.linting
.link checking

nodemon and grunt plugin

#Page testing
embed tests in the page itself.

npm install --save-dev mocha
vs
npm install --save mocha

#chai assertion library

#request object
req.params
req.param(name)
req.query
req.body
req.route
req.cookies/req.signedCookies
req.headers
req.accepts([types])
req.ip
req.path
req.host
req.xhr
req.protocol
req.secure
req.url/req.originalUrl
req.acceptedLanguages

#Response object
res.status(code)
res.set(name,value)
res.cookie(name,value, [options], res.clearCookie(name,[options]))
res.redirect([status],url)
res.send(body),res.send(status,body)
res.json(json),res.json(status,json)
res.jsonp(json),res.jsonp(status,json)
res.type(type)
res.format(object)
res.attachment([filename]),res.download(path,[filename],[callback])
res.sendFile(path,[options],[callback])
res.links(links)
res.locals,res.rendr(view,[locals],callback)

#Firstcheck the Express API documentation, then Express source, finally Node documentation
.lib/application.js
.lib/express.js
.lib/request.js
.lib/response.js
.lib/router/route.js

#Rendering content
res.send //test page
res.render //content
req.query, req.session, req.cookie/req.signedCookies

app.get('/greeting', function(req, res){ res.render('about', {
                message: 'welcome',
                style: req.query.style,
                userid: req.cookie.userid,
                username: req.session.username,
}); });

#sites
.themeforest
.wrapbootstrap

#mailing
##nodemailer
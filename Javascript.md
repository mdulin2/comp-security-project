# Web Security Injections and Issues

## Cross-Site Scripting 
XSS is a class of attacks that involve injecting client side scripts through the website which then renders to other users. 

A famous example is the self retweeting heart;  

``` html
<script class="xss">$('.xss').parents().eq(1).find('a').eq(1).click();$('[data-action=retweet]').click();alert('XSS in Tweetdeck')</script>♥
```

This attack took advantage of the fact that TweetDeck, a 3rd party Twitter client didn't have any filtering for javascript inside of tweets. In general, it was assumed that the Twitter backend handled this, but unfortunately they did not either.

Let's break down each part of this tweet to see what's up. 

The first `<script class="xss">` defines a special HTML element that allows the execution of javascript code on the page. It also defines a "class" which serves as a label that we can point back to in a moment. 

Then, we'll take advantage of jquery to find "ourselves" (or the script tag) with `$('.xss')`. Then we'll grab the first parent element with `.parents().eq(1)`. This then lets us look for a link, or "anchor" with `.find('a').eq(1)`. 

This link happens to be the "retweet" button. So we'll click it: `.click()`. We can then confirm the action with `$('[data-action=retweet]').click()`. 

Since the original creator was not malicious and simply trying to expose a vulnerability, he pops up an alert: `alert('XSS in Tweetdeck')`. 

Then finally, we close the script and add a heart for flair: `</script>♥`.

<h2>First of all: What are the use cases?</h2>
<p>It's probably most useful for websites without an API. With headless browsers like Puppeteer there is almost always a way.</p>

<h2>Let's try Puppeteer out</h2>
<p>
  In order to use Puppeteer, we have to install Puppeteer first. We can do this by typing 
  <i>npm i puppeteer</i>.
</p>
<p>Let's try a real-world example now and get the featured article on dev.to:</p>

<h3>First we need to import Puppeteer, start Puppeteer &amp;<br>create a new page, a equivalent to a tab in a regular browser:</h3>
<code>const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
})();</code>

<h3>Now we can browse to dev.to</h3>
<code>await page.goto('https://dev.to/');</code>

<h3>...and get the featured article</h3>
<code>const featuredArticle = await page.evaluate(() => document.querySelector('.big-article h3').innerText);
console.log(featuredArticle); // '9 Evil Bash Commands Explained'</code>


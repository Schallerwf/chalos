# chalos
Real hackers order empanadas from the CLI.

```bash
pip install chalos
```

## How it Works / Why I Built it
Square provides an API that can be used to create checkout links using your menu.

I became friends with the owners of Chalos up the street and they were kind enough to give me API access when I joked around about building this.

This CLI tool makes a call to an AWS lambda which loads the current state of their menu. This way they can mark things as out of stock the same way they do right now and this tool can produce a correct menu. Next, the CLI allows you to build a cart for checkout. Another lambda endpoint is used to take your cart and generate a unique checkout URL using Squares API. The url is returned to the your CLI and it opens automatically in your browser to complete the order. 

The tricky part was navigating the square menu. You can imagine that an evolving menu over the past few years across two locations with different modifications (e.g, no cheese, extra cheese) and different sizes, etc creates quite a massive catalog of ids. So to go from 'Breakfast Burrito with Avocado' to the correct set of ids that square needs to generate the checkout page was mostly the challenge. I built this mapping by hand by looking at their menu and looking up the id in a catalog dump I generated from Square API calls. This mapping now lives in the lambda and takes the string based cart and converts it into the id based dictionary square wants. 

If they change their menu, then the CLI tool will require an update. The next level of effort here will be the CLI responding more dynamically to changes in the menu without needing coding changes, so that this can live and work without maintaince for longer periods of time.

I ran into some issues with this not working across different OS. I wanted to keep dependencies minimal but still have a fun/silly CLI experience. I had built CLI tools for work many times but this was a fun change of pace and a nice chance to try some different idea. I think it came out nice.

I also recently tried using claude to produce the mapping of product ids and it did what took me a few hours in about 3 minutes. 

## About Chalos
Chalos is a local empanada and coffee shop in San Francisco. I got to know the owners over the last few years. They are great people and make great food. When they opened a second location under Salesforce tower in SF, I thought it might be fun to have a CLI tool for ordering. They were kind enough to give me access to their square API and I built this as a fun little side project where I could play around with some new things. Thank you for checking it out and I hope you enjoy what Chalos has to offer.
Willy

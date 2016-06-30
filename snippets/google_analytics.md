# Google Analytics

We have a bit of a mix of implementations, so next time you work on a site, please take 30 secs to update it to the new standard, which is referred to as `analytics.js` (old system was `ga.js`).

```javascript
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

// replace auto with a domain name if you want to fake it
ga('create', '<property_id>', 'auto');
// enable better demographics and DFP linking
ga('require', 'displayfeatures');
// enable better link attribution ('heatmaps')
ga('require', 'linkid', 'linkid.js');

// optionally set some custom dimensions
//ga('set', "dimension<X>", "<val>");

// register the pageview with GA
ga('send', 'pageview');
```

Optionally, elsewhere on site, in event handlers:

```
// fire an event
ga('send', 'event', 'comments', 'posted');

// optionally track a tweet event
ga('send', 'social', {
  'socialNetwork': 'twitter',
  'socialAction': 'tweet',
  'socialTarget': '<page_url>'
} );
```

This snippet sets up tracking in the default namespace.  If you need to run more than one tracker (e.g. for a separate account for a 3rd party) then you need to use a namespace for at least one of the accounts. It's ok to namespace all accounts if you want. To do that, just init trackers thus, in the same script block:

```
ga('create', '<property_id_1>', 'auto', {'name': 'mytracker1'});
ga('create', '<property_id_2>', 'auto', {'name': 'mytracker2'});

// prefix ALL sends, requires, set commends, etc, with namespace:
ga('mytracker1.send', 'pageview');
ga('mytracker2.send', 'pageview');
```

You can see available custom dimensions for a site in the admin interface, in Accounts -> Property -> Custom Definitions -> Custom Dimensions.

Event tracking is especially useful, please see [this documentation](https://developers.google.com/analytics/devguides/collection/analyticsjs/events)

# bradley-tower-static

This is the Mayor's Dashboard for the City of Los Angeles. It is a static website - just html pages - built using Sheetsee.js and Tabletop, that requires very little programming or customization to stand up. The data is stored in Google Docs. 

This is the live, operational dashboard for the mayor of Los Angeles, which any city is welcome to use and customize. It has been built to be decidely simple to deploy and maintain; it is free and open source, can be hosted freely on GitHub, and is powered by Google Docs (another free solution). 

There are two key functional elements to the dashboard: 

1. **"Metric Cards"**: Simple, quick-to-understand boxes for each key metrics (either overall or for a specific department/issue); these include a goal, a current status, a delta, and an editorial indication of progress (eg red, green). These are entirely built via the Google Sheets integration, and dynamically updated by any changes to those spreadsheets.
2. **Visualizations**: Interactive charts, graphs, an maps that provide deep dives into key policy/issue areas. These are typically manually built using D3 or CartoDB, though some charts are dynamically created by API integrations with Socrata; do note: most if not all are manually updated, in line with the city's performance management unit/process.

The City of Los Angeles has enhanced this version with some additional functionality, which while technically a bit more tricky, does enable easier content and page management: http://github.com/datala/bradley-tower

## Architecture / How Things Work

The core technology is TableTop.js, Bootstrap, Sheetsee.js, and Jekyll -- all client side software, which won't require a server or must work to get going. 

* **Tabletop.js / Sheetsee.js**: Javascript plugins designed to easily pull data from Google Spreadsheets on the client side and build dynamic pages -- think using Google Sheets as a lightweight database that's easily editable by non-technical staff
* **Bootstrap**: Very popular design framework
* **D3** (by DevExpress): Custom varient of D3 with additional animations for visualizations

## Deploying the Dashboard

There are two versions of the Dashboard: this is the static HTML repository, which makes it rather straightforward to redeploy but harder to update, and then a Jekyll-based CMS style app. (See here for documentation on deploying the latter, which does require some local software, technical understanding, etc.)

### Redeploying the site locally

```
[Fork this repository](https://github.com/datala/bradley-tower/fork)
Run the jekyll server: `jekyll serve`
```

### Deploying to Github

The site is hosted on GitHub using Github Pages. This means it comes at no cost and requires no internal hosting. Simply push changes to a branch "gh-pages" and those will be available live at [username].github.io/bradley-tower

### Setting up the Data

All of the data for the "metric cards" comes from a specific Google Sheet for each page on the dashboard:

<img src="http://datala.github.io/bradley-tower/img/gdocs.png" width=700 alt="Screenshot of GDocs Template">

It's important to keep the formatting/headers from the spreadsheet. You can grab a copy of the spreadsheet here and copy to your own Google Docs account. 

1. Go to the [Google Sheets template](https://drive.google.com/previewtemplate?id=1e2CJALC8PR7CrPeI0mjygmVjdPd905XLjwzaTuNRXK0&mode=public)
2. Select "Use this template" to save a working copy to your account
3. Select File - Publish to the Web, and copy the SheetID from the provided url (e.g. 1ZVxlgt9couygM7bzteI3YMX8OSE-jnfZAssTb8xUQ2Q)

Note: the icon column relies on the popular, open, and free icons from Linecons and Font Awesome.

### Connecting the data to the dashboards

The basic content structure of the site is two fold: 

1. Top sheet: This features all the key visualizations in one page on the homepage; as mentioned above, these are fairly custom visualizations that are stored in /_includes/viz to ensure easy recall from page to page.
2. Dashboard pages: These pages rely on the Google Sheets integration and are stored in /_posts. To create a new page, simply duplicate an existing one and edit the following portion of code:

```
<script type='text/javascript'>
	document.addEventListener('DOMContentLoaded', function() {
		var URL = ''[YOUR GOOGLE SHEETS ID]''
		Tabletop.init( { key: URL, callback: showInfo, simpleSheet: true, } )
```


Please reach out to @abhinemani if you're interested in helping out or redeploying it. 


# TripAdvisor Scraper Actor

## What is TripAdvisor Scraper actor?
The TripAdvisor Scraper Actor is a simple tool that helps you collect travel info from TripAdvisor easily. It's great for finding out about places to stay, eat, visit, or explore, making data gathering a breeze for everyone, without any coding skills needed.

### Key features
- 🔍 **Easy Searches**: Start by choosing what you're interested in, like hotels or restaurants, and even use a specific TripAdvisor URL page to get exactly what you need.
- 📅 **Pick Dates**: You can choose check-in and check-out dates to see availability or prices for your trip.
- 🌐 **Your Preferences Matter**: Set it up in your language and currency, making the data gathered immediately useful.
- 📚 **Find Comprehensive Info**: From eateries and hotels to thrilling attractions and activities, extract a wide array of information. Where available, secure direct contact details to facilitate outreach.


## Use Cases | Who Can Use TripAdvisor Scraper
- Hospitality Analysts and **Market Researchers** seeking deep dives into consumer trends and industry benchmarks.
- **Travel Professionals and Vacation Planners** aim to craft the ultimate travel experience with up-to-the-minute information.
- Digital Nomads and Travel Writers looking for the next story or **hidden gem, requiring authentic and detailed descriptions** of locales.
- Innovators and App Developers in need of a robust dataset for building **travel-related applications or analytics platforms**.

## Input
Either start with a keyword or specific store URLs to your research.

💡When you want to scrape over a specific list URL, just copy and paste the link as one of the startUrl.

![](https://cdn.epctex.com/actors/tripadvisor/1.png)

You can choose the check-in and check-out dates for your research. Also, if you start with a keyword, don’t forget that you can include Attractions, Restaurants, Hotels, and Vacation Rentals.

![](https://cdn.epctex.com/actors/tripadvisor/2.png)

You can localize your search on language and currency.

![](https://cdn.epctex.com/actors/tripadvisor/3.png)

You can limit the number of output results by either writing a number for number of listing items or list end page.

💡If you would like to scrape only the first page of a list then put the link for the page and have the endPage as 1.

💡With the last approach that is explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the endPage parameter as 6 then you'll have the 5th and 6th pages only.

![](https://cdn.epctex.com/actors/tripadvisor/4.png)

It is recommended to keep the other options as default.

![](https://cdn.epctex.com/actors/tripadvisor/5.png)

### Input Parameters Explained
The input of this scraper should be JSON containing the list of pages on TripAdvisor that should be visited. Required fields are:

- `search`: (Optional) (String)

	A string specifying the name of a location for a Tripadvisor search, such as a country, city, or neighborhood. The scraper selects the first 'Location' type result based on this input.
- `checkInDate`: (Optional) (String)

	The hotel check-in date to view specific offers. Leave blank to see default offers.
- `checkOutDate`: (Optional) (String)

	The hotel check-out date for precise offer durations.
- `includeAttractions`: (Optional) (Boolean)

	Search will include the attractions.
- `includeRestaurants`: (Optional) (Boolean)

	Search will include the restaurants.
- `includeHotels`: (Optional) (Boolean)

	Search will include the hotels.
- `includeVacationRentals`: (Optional) (Boolean)

	Search will include the vacation rentals.
- `startUrls`: (Optional) (Array)

	List of TripAdvisor URLs. You should only provide TripAdvisor list or detail URLs.
- `language`: (Optional) (String)

	Language for the TripAdvisor to change the results accordingly.
- `currency`: (Optional) (String)

	Currency for the TripAdvisor to change the results accordingly.
- `endPage`: (Optional) (Number)

	Final number of page that you want to scrape. The default is Infinite. This applies to all search requests and startUrls individually.
- `maxItems`: (Optional) (Number)

	You can limit scraped items. This should be useful when you search through the big lists or search results.
- `proxy`: (Required) (Proxy Object)

	Proxy configuration.
- `extendOutputFunction`: (Optional) (String)

	A function that takes a JQuery handle ($) as an argument and returns an object with data.
- `customMapFunction`: (Optional) (String)

	A function that takes each object's handle as an argument and returns the object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).


### TripAdvisor Scraper Input Examples
![](https://cdn.epctex.com/actors/tripadvisor/6.png)

```json
{
  "startUrls":[
    "https://www.tripadvisor.com/Hotel_Review-g35805-d236299-Reviews-Sofitel_Chicago_Magnificent_Mile-Chicago_Illinois.html",
    "https://www.tripadvisor.com/Hotels-g294200-Egypt-Hotels.html"
  ],
  "search": "New York",
  "checkInDate": "2025-01-01",
  "checkOutDate": "2025-10-01",
  "includeAttractions": true,
  "includeRestaurants": true,
  "includeHotels": true,
  "includeVacationRentals": true,
  "language": "en",
  "currency": "USD",
  "maxItems": 100,
  "endPage": 1,
  "extendOutputFunction": "($) => { return {} }",
  "customMapFunction": "(object) => { return {...object} }",
  "proxy": {
    "useApifyProxy": true
  }
}
```

### Compute Unit Consumption
The actor is optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detailed requests. If the actor doesn't block very often it'll scrape 100 listings in 20 seconds with ~$0.005-$0.006 compute units.

## Bugs, fixes, updates, and changelog
This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/tripadvisor-scraper/issues).


## During the Run
During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with a failure state and output an explanation of what is wrong.

## Output

### Restaurant
```json
{
	"id": "1049685",
	"type": "restaurant",
	"category": "restaurant",
	"subcategories": [
		"Sit down"
	],
	"name": "Benoit New York",
	"locationString": "New York City, New York",
	"description": "Restaurant, Wine Bar & Private Dining - Open since 2008, Benoit New York is the third member of internationally-acclaimed Chef Alain Ducasse's Benoit family - which also includes the bistro in Paris since 1912 and Benoit Tokyo. In New York, guests enjoy a warm and authentic experience and a menu filled with traditional bistro dishes with a modern flair. In August 2016, the restaurant underwent a renovation, bringing a contemporary New York City touch to the classic French restaurant.",
	"image": "https://media-cdn.tripadvisor.com/media/photo-o/0d/7c/2f/fb/hors-d-oeuvre.jpg",
	"photoCount": 383,
	"awards": [],
	"rankingPosition": 627,
	"rating": 4,
	"rawRanking": 4.039697647094727,
	"phone": "+1 646-943-7373",
	"address": "60 W 55th St Between Fifth & Sixth Aves, New York City, NY 10019-5308",
	"addressObj": {
		"street1": "60 W 55th St",
		"street2": "Between Fifth & Sixth Aves",
		"city": "New York City",
		"state": "NY",
		"country": "United States",
		"postalcode": "10019-5308"
	},
	"localName": "Benoit New York",
	"localAddress": "60 W 55th St, Between Fifth & Sixth Aves, 10019-5308",
	"localLangCode": "en-US",
	"email": "bistrot@benoitny.com",
	"latitude": 40.76269,
	"longitude": -73.97744,
	"webUrl": "https://www.tripadvisor.com/Restaurant_Review-g60763-d1049685-Reviews-Benoit_New_York-New_York_City_New_York.html",
	"website": "http://www.benoitny.com/",
	"rankingString": "#627 of 14,183 places to eat in New York City",
	"rankingDenominator": "8205",
	"neighborhoodLocations": [
		{
			"id": "7102352",
			"name": "Midtown"
		}
	],
	"nearestMetroStations": [
		{
			"name": "57th St",
			"localName": "57th St",
			"address": "1392-1394 6th Ave, Long Island City, NY 10019",
			"localAddress": "1392-1394 6th Ave, 10019",
			"lines": [
				{
					"id": "new-york-new-york-city-subway-f",
					"lineName": "F",
					"lineSymbol": "https://static.tacdn.com/img/api/metro_stations/metro_placeholder.png",
					"systemName": "NYC Subway",
					"systemSymbol": "https://static.tacdn.com/img/api/metro_stations/metro_placeholder.png",
					"type": "Rapid Transit"
				}
			],
			"latitude": 40.76396942138672,
			"longitude": -73.97745513916016,
			"distance": 0.08839800240055308
		}
	],
	"ancestorLocations": [
		{
			"id": "60763",
			"name": "New York City",
			"abbreviation": null,
			"subcategory": "City"
		}
	],
	"ratingHistogram": {
		"count1": 35,
		"count2": 47,
		"count3": 128,
		"count4": 301,
		"count5": 470
	},
	"numberOfReviews": 981,
	"priceLevel": "$$$$",
	"priceRange": "$25 - $100",
	"cuisines": [
		"French",
		"Contemporary"
	],
	"mealTypes": [
		"Lunch",
		"Dinner"
	],
	"dishes": [
		"Baguette",
		"Filet Mignon",
		"Lobster"
	],
	"dietaryRestrictions": [
		"Vegetarian Friendly",
		"Gluten Free Options"
	],
	"establishmentTypes": [
		"Restaurants"
	],
	"menuWebUrl": "https://www.benoitny.com/menus",
	"isClosed": false,
	"isLongClosed": false,
	"hours": {
		"weekRanges": [
			[
				{
					"open": 720,
					"openHours": "12:00",
					"close": 1260,
					"closeHours": "21:00"
				}
			]
		],
		"timezone": "America/New_York"
	},
	"booking": {
		"provider": "OpenTable",
		"url": "https://www.tripadvisor.com/Commerce?p=OpenTable&src=232171538&geo=1049685&from=api&area=reservation_button&slot=1&matchID=1&oos=0&cnt=1&silo=45582&bucket=979641&nrank=1&crank=1&clt=R&ttype=Restaurant&tm=288266674&managed=false&capped=false&gosox=9DMvibDTWdNaFeGYL8QTakyv1LBYZaGpeB4MEHn-hv2mZBN376EHVCGusTIRxmJ8AObDCfP9_-JSKy-iI9MlddieEOHSA0Xrk7G74dAg8PM&cs=18e91e712bfe3b841eba52767082a89f5"
	}
}
```

### Hotel
```json
{
	"id": "262330",
	"type": "hotel",
	"category": "hotel",
	"subcategories": [
		"Hotel"
	],
	"name": "Millennium Downtown New York",
	"locationString": "New York City, New York",
	"description": "Millennium New York Downtown is located in the heart of the Financial District, just steps from The Oculus, One World Observatory, and the 9/11 Memorial & Museum. Guests love our City View rooms and suites, featuring some of the best views in Lower Manhattan: unobstructed views overlooking the Oculus NYC and One World Trade Center to the West, and the iconic Woolworth Building and Brooklyn Bridge in East-facing rooms. With 11 subway stops within a block of the property and ferry access just a 10 minute walk away, we're also one of the most convenient hotels in the city, offering easy access to Times Square, Madison Square Garden, Downtown Brooklyn, and all 5 boroughs. Iconic attractions like Wall Street, City Hall, Brooklyn Bridge, and the South Street Seaport are within a half mile.",
	"image": "https://media-cdn.tripadvisor.com/media/photo-o/29/52/3c/b1/manhattan-sky-view.jpg",
	"photoCount": 3015,
	"awards": [],
	"rankingPosition": 411,
	"rating": 4,
	"rawRanking": 3.164475440979004,
	"phone": "+1 212-693-2001",
	"address": "55 Church Street, New York City, NY 10007",
	"addressObj": {
		"street1": "55 Church Street",
		"street2": "",
		"city": "New York City",
		"state": "NY",
		"country": "United States",
		"postalcode": "10007"
	},
	"localName": "Millennium Downtown New York",
	"localAddress": "55 Church Street, 10007",
	"localLangCode": "en-US",
	"email": "reservations@millenniumdowntownnyc.com",
	"latitude": 40.711433,
	"longitude": -74.01038,
	"webUrl": "https://www.tripadvisor.com/Hotel_Review-g60763-d262330-Reviews-Millennium_Downtown_New_York-New_York_City_New_York.html",
	"website": "https://www.millenniumhotels.com/en/new-york/millennium-downtown-new-york/",
	"rankingString": "#411 of 542 hotels in New York City",
	"rankingDenominator": "542",
	"neighborhoodLocations": [
		{
			"id": "15565677",
			"name": "Downtown Manhattan (Downtown)"
		}
	],
	"nearestMetroStations": [
		{
			"name": "Cortlandt St",
			"localName": "Cortlandt St",
			"address": "19 Church St, New York City, NY 10007",
			"localAddress": "19 Church St, 10007",
			"lines": [
				{
					"id": "new-york-new-york-city-subway-r",
					"lineName": "R",
					"lineSymbol": "https://static.tacdn.com/img/api/metro_stations/metro_placeholder.png",
					"systemName": "NYC Subway",
					"systemSymbol": "https://static.tacdn.com/img/api/metro_stations/metro_placeholder.png",
					"type": "Rapid Transit"
				}
			],
			"latitude": 40.71066665649414,
			"longitude": -74.01103210449219,
			"distance": 0.06300009596063123
		}
	],
	"ancestorLocations": [
		{
			"id": "60763",
			"name": "New York City",
			"abbreviation": null,
			"subcategory": "City"
		}
	],
	"ratingHistogram": {
		"count1": 477,
		"count2": 516,
		"count3": 1055,
		"count4": 2131,
		"count5": 2531
	},
	"numberOfReviews": 6710,
	"hotelClass": "4.0",
	"hotelClassAttribution": "This property is classified according to Giata.",
	"amenities": [
		"Room service",
		"Fitness center"
	],
	"priceLevel": "$$$",
	"priceRange": "$177 - $341",
	"roomTips": [
		{
			"user": {
				"userId": "96E2FA3F61227B32D609734C7C222EE7",
				"type": "user",
				"username": "W5540ABmichaelb",
				"userLocation": {
					"name": "New York City, New York",
					"id": "60763"
				},
				"avatar": "https://media-cdn.tripadvisor.com/media/photo-l/1a/f6/eb/43/default-avatar-2020-11.jpg",
				"link": "https://www.tripadvisor.com/MemberProfile-a_uid.96E2FA3F61227B32D609734C7C222EE7",
				"points": 0,
				"createdTime": "2014-02-06T11:34:02-0500"
			},
			"type": "room_tip",
			"text": "Avoid this hotel - price point is good but experince is distressing and upsetting.",
			"rating": 1,
			"reviewId": "938914393",
			"id": "938914393",
			"createdTime": "2024-02-19T07:33:15-05:00"
		}
	],
	"isClosed": false,
	"isLongClosed": false,
	"images": [
		"https://media-cdn.tripadvisor.com/media/photo-o/29/52/3c/b1/manhattan-sky-view.jpg",
		"https://media-cdn.tripadvisor.com/media/photo-m/1280/22/43/cb/4e/view-from-a-room.jpg",
		"https://media-cdn.tripadvisor.com/media/photo-o/12/9a/28/76/liquid-assets-lobby-bar.jpg"
	],
	"numberOfRooms": 569,
	"offers": [
		{
			"priceText": "$132",
			"taxesAndFeesText": "$58",
			"totalStayPriceText": "$51,870",
			"priceBeforeSale": null,
			"provider": "Expedia",
			"vendor": "Expedia.com",
			"canPayInInstallments": true
		}
	],
	"reviewTags": [
		{
			"text": "freedom tower"
		},
		{
			"text": "millennium hilton"
		}
	],
	"checkInDate": "2025-01-01",
	"checkOutDate": "2025-10-01"
}
```

### Attraction
```json
{
	"id": "282090",
	"type": "attraction",
	"category": "attraction",
	"subcategories": [
		"Sights & Landmarks"
	],
	"name": "New York State Capitol",
	"locationString": "Albany, New York",
	"description": "The New York State Capitol has served as the seat of government for New York since the 1880's. Over 125 years old, the building is a marvel of late 19th-century architectural grandeur. Built by hand of solid masonry, it took 5 architects and 32 years to complete. Over the years meticulous restoration has been done to maintain and protect the Capitol for future generations of New Yorkers.",
	"image": "https://media-cdn.tripadvisor.com/media/photo-o/0b/ae/8c/6d/new-york-state-capitol.jpg",
	"photoCount": 735,
	"awards": [],
	"rankingPosition": 2,
	"rating": 4.5,
	"rawRanking": 4.156702041625977,
	"phone": "+1 518-474-2418",
	"address": "State St., Albany, NY 12207",
	"addressObj": {
		"street1": "State St.",
		"street2": "",
		"city": "Albany",
		"state": "NY",
		"country": "United States",
		"postalcode": "12207"
	},
	"localName": "New York State Capitol",
	"localAddress": "State St., 12207",
	"localLangCode": "en-US",
	"email": "Plaza.Visitor.Center@ogs.ny.gov",
	"latitude": 42.652542,
	"longitude": -73.7574,
	"webUrl": "https://www.tripadvisor.com/Attraction_Review-g29786-d282090-Reviews-New_York_State_Capitol-Albany_New_York.html",
	"website": "http://www.empirestateplaza.ny.gov",
	"rankingString": "#2 of 84 things to do in Albany",
	"rankingDenominator": "84",
	"nearestMetroStations": [],
	"ancestorLocations": [
		{
			"id": "29786",
			"name": "Albany",
			"abbreviation": null,
			"subcategory": "City"
		},
		{
			"id": "28953",
			"name": "New York",
			"abbreviation": "NY",
			"subcategory": "State"
		},
		{
			"id": "191",
			"name": "United States",
			"abbreviation": null,
			"subcategory": "Country"
		}
	],
	"ratingHistogram": {
		"count1": 3,
		"count2": 3,
		"count3": 37,
		"count4": 204,
		"count5": 618
	},
	"numberOfReviews": 865,
	"isClosed": false,
	"isLongClosed": false,
	"hours": {
		"weekRanges": [
			[],
			[
				{
					"open": 420,
					"openHours": "07:00",
					"close": 1140,
					"closeHours": "19:00"
				}
			],
			[
				{
					"open": 420,
					"openHours": "07:00",
					"close": 1140,
					"closeHours": "19:00"
				}
			],
			[
				{
					"open": 420,
					"openHours": "07:00",
					"close": 1140,
					"closeHours": "19:00"
				}
			],
			[
				{
					"open": 420,
					"openHours": "07:00",
					"close": 1140,
					"closeHours": "19:00"
				}
			],
			[
				{
					"open": 420,
					"openHours": "07:00",
					"close": 1140,
					"closeHours": "19:00"
				}
			],
			[]
		],
		"timezone": "America/New_York"
	},
	"booking": {
		"provider": "Viator",
		"url": "https://www.tripadvisor.com/Commerce?url=https%3A%2F%2Fwww.viator.com%2Ftours%2FAlbany%2FLets-Roams-Albany-Scavenger-Hunt-Empire-State-Of-Mind%2Fd23070-104204P22%3Feap%3Dtripadvisor-main-11383%26aid%3Dtripen1&partnerKey=1&urlKey=2aa6884054dd6d3f2&logme=true&uidparam=refid&attrc=true&Provider=Viator&area=TOP&slot=1&cnt=1&geo=282090&clt=TD&from=api&nt=true"
	},
	"offerGroup": {
		"lowestPrice": "$0.12",
		"offerList": [
			{
				"url": "https://www.tripadvisor.com/Commerce?url=https%3A%2F%2Fwww.viator.com%2Ftours%2FAlbany%2FLets-Roams-Albany-Scavenger-Hunt-Empire-State-Of-Mind%2Fd23070-104204P22%3Feap%3Dtripadvisor-main-11383%26aid%3Dtripen1&partnerKey=1&urlKey=2aa6884054dd6d3f2&logme=true&uidparam=refid&attrc=true&Provider=Viator&area=viator_multi&slot=1&cnt=1&geo=282090&clt=TD&from=api&nt=true",
				"price": "$12.31",
				"roundedUpPrice": "$13",
				"offerType": "",
				"title": "Albany Scavenger Hunt: Empire State Of Mind",
				"productCode": "104204P22",
				"partner": "Viator",
				"imageUrl": "https://media.tacdn.com/media/attractions-splice-spp-360x240/09/17/31/14.jpg",
				"description": null,
				"primaryCategory": "Self-guided Tours & Rentals"
			}
		]
	}
}
```

### Vacation Rental
```json
{
	"id": 7164901,
	"type": "vacationRental",
	"webUrl": "https://www.tripadvisor.com/VacationRentalReview-g48808-d7164901.html",
	"name": "Beautiful Estate home in the Hamptons, New York",
	"latitude": 40.944626,
	"longitude": -72.36356,
	"rating": -1,
	"description": "This beautiful estate home in Water Mill, New York borders the prestigious Matt Lauer's 40 acre horse farm with distant ocean views.  This estate features 7 bedrooms with 7 en suite bathrooms, 2 1/2 baths, two master bedrooms.  There are five full masonry fireplaces, pool room, wine room, cigar room, 15 seated high dif theater, sauna with dressing and shower facilities.  Outdoors features a 60 foot free form gunite pool with 7 person spa with waterfall, outdoor shower.  There is a sunken in all weather tennis court with stone walls, separate maids quarters, mature landscaping, and wrought iron gates complete this package.",
	"image": "https://media-cdn.tripadvisor.com/media/vr-splice-j/01/46/b5/ab.jpg",
	"photos": [
		{
			"url": "https://media-cdn.tripadvisor.com/media/vr-splice-l/01/46/b5/ab.jpg",
			"description": "front of estate"
		},
		{
			"url": "https://media-cdn.tripadvisor.com/media/vr-splice-l/01/46/b5/aa.jpg",
			"description": "free form pool with waterfall hottub"
		}
	],
	"numberOfReviews": 0,
	"numberOfRooms": 7,
	"baseDailyRate": {
		"amount": 6914,
		"currency": "USD"
	},
	"bedroomInfo": "",
	"bathroomInfo": "7 Full baths",
	"bathCount": 7,
	"features": [
		{
			"feature": "DVD player",
			"hasFeature": true
		},
		{
			"feature": "Air conditioning",
			"hasFeature": true
		}
	]
}
```

## FAQ
**🤔 How can I specify what to search for?**<br/>
The actor provides a rich set of customization options, from keywords 🔑 and category selection 🏷️ to precise control over dates 📅, language 🌍, and currency 💵, enabling highly targeted searches.

**🌐 Is it possible to scrape data using a specific URL?**<br/>
Absolutely! Initiating your data extraction with a specific TripAdvisor page URL 🖥️ is fully supported, offering pinpoint accuracy in your scraping endeavors.

**📚 What categories of information does the scraper cover?**<br/>
It adeptly pulls detailed listings on a broad spectrum of travel-related categories ✈️🏨🍴, including the potential to gather direct contacts 📞📧 when openly available.

**🌍 How does it adapt to my regional preferences?**<br/>
Yes, you can set it to show info in your preferred language 🗣️ and currency💲.

**📝 If I want to scrape reviews, what should I do?**<br/>
For scraping reviews, we have another product specifically designed for this purpose: [TripAdvisor Reviews Scraper](https://apify.com/epctex/tripadvisor-reviews-scraper?fpr=yhdrb) 🌟. This dedicated tool is tailored to efficiently collect review data from TripAdvisor, ensuring you have access to comprehensive feedback and insights.

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that are available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.

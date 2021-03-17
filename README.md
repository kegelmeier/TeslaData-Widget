# TeslaData Widget for TeslaMate
A Scriptable widget to pull data from a given API by TeslaMate and TeslaMateAPI to display a widget on your iPhone. 

<img src="documentation/screen_001.png" width="400" /> &nbsp; <img src="documentation/screen_003.png" width="400" /> &nbsp; <img src="documentation/screen_001_med.png" width="400" />

## Usage
### Install with Scriptdude

[<img src="https://scriptdu.de/download.svg" width="120" />](https://scriptdu.de/?name=TeslaData&source=https://raw.githubusercontent.com/DrieStone/TeslaData-Widget/main/TeslaData%20Widget.js&docs=https://github.com/DrieStone/TeslaData-Widget#generator)

### Manual Install

* Get Scriptable in the Apple App Store.
* Download the `TeslaData Widget.js` file to your iCloud/Scriptable folder (or create a new widget in the scriptable app).
* Create a small scriptable widget.
* Link your API do one of the following
    * Under widget options, select "TeslaData Widget" and enter the API url into the widget parameters.
    * If you're using TeslaFi, you can just enter the API Key in the widget paramters.
    * For advanced users (or if you want to extend the functionality of TeslaData), you should create a parameters.js file in iCloud (see Optional below).

### Manual Update

* Replace the `TeslaData Widget.js` in your iCloud/Scriptable folder with the one here.
* Wait 5-7 minutes for Scriptable to grab the new file and update the widget.

### Optional/Advanced
* Download/create the tesla_data directory to your iCloud/Scriptable folder.
* Create a paramters.js file (or copy the one from here), and add your API url to the file.
* Get a [map API key from MapQuest](https://developer.mapquest.com/) and add it to your paramters.js file.
* Install any themes into the tesla_data folder, and modify the parameters.js file to include the theme you'd like to apply (e.g. custom_theme = "3d" will load the 3d.js theme from the themes directory).
* Note: The widget parameter overrides the parameters.js. This is so you can have widgets for more than one car (or more than one data source).

### Other API
If you use other tools like [TeslaLogger](https://github.com/bassmaster187/TeslaLogger), [Tronity](https://tronity.io/home/5OiA7SfA), etc. you only have to provide [json file](documentation/sample.json) with the following data ([more details on the required fields](documentation/json_requirements.md)):

`
{
   "response":null,
   "battery_level":27,
   "usable_battery_level":26,
   "charge_limit_soc":90,
   "carState":"Idling",
   "Date":"2020-10-28T14:57:15Z",
   "sentry_mode":0,
   "display_name":"Name",
   "locked":1,
   "is_climate_on":0,
   "inside_temp":14.6,
   "driver_temp_setting":22.0,
   "measure":"km",
   "est_battery_range":90.605842,
   "battery_range":125.2227454,
   "time_to_full_charge":0.0,
   "fast_charger_type":"<invalid>"
}
`

API url (eg.): https://MY_USER:MY_PASS@MY_URL.com/api.json

## Map

At medium sizes, the widget will show a map with the location of the car, but only if your API includes long/lat and you have a key from MapQuest. Visit https://developer.mapquest.com/ to create an account and get an API. Then, add the API key in your parameters.js file.

## Configuration

There are a few options if you want to turn on/off battery percentage and estimated range (and if you'd like to use the car's range, or the TeslaFi estimate). These options are the constants at the top of the file (set the variables as true/false)

Note, due to the lag with TeslaFi pulling data from your car, and the lag of iOS pulling the data, the resulting display could be ~5 minutes stale (and the data could be hours or even a day old because TeslaFi lets the car sleep, so its not sending data)

## Features

This should support:
* charging overview (current charge, charge limit, and time until charge complete)
* conditioning on indicator
* doors locked/unlocked
* interior temperature
* sentry mode on
* sleeping, idle, driving indicator
* time since the data was retreived from the car (respects TeslaFi sleep)
* map location of the car's current position

## Themes

To add themes to TeslaData you need to add theme files to the tesla_data file, and modify the custom_theme variable at the top of the widget code. To get an overview of themes, you can look at the [Theme Listing](documentation/theme_listing.md) page.

## Outstanding Bugs

- There appears to be an issue with SF graphics in Scriptable where the images are stretched.
- Dark mode doesn't currently work for widgets in Scriptable.

## Notes for Developers

Starting with v1.5 TeslaData now supports theming. The theme file is loaded right before the widget is drawn and displayed, so the theme can override any existing code (so you can change how things work without worrying about your code being overwritten with future updates of Tesla Data).

Note: due to the way themes are includes, debugging information from Scriptable is lacking. For testing purposes, it is probably best to develop by adding code to the end of the main Javascript file, and moving the code to a theme file once the code is running properly.

Starting with v1.5 The all colors are defined as an obect at the top of the file. These can be overriden if you want to make changes (you should use a theme file for this).

Starting with v1.5 TeslaData will optionally pull JSON files from iCloud for testing purposes. Place your JSON files in the tesla_themes directory on iCloud, and tell the widget to pull the data by modifying the debug_data string (i.e. debug_data = "standard" will load the "standard.json" file and ignore the URL).

You can inject your own code without affecting the TeslaData codebase via theming and/or parameters.js The parameters are loaded after the default values are set but before data is pulled from the API. The theme is loaded right before the widget is rendered, but after the data is loaded and processed. You can use the parameters.js file to inject code to change the way that code is loaded. You can create a car_data.postLoad function that will recieve the json from the API (so you can affect the information loaded into the car_data object before it's acted on).


## Changelog

- v0.1 
   - Initial release added to GitHub  

# react-naitve-tutorial
This tutorial is absolutely based on React Native's official tutorial + Appcoda's tutorial. You can find them at:

1. https://facebook.github.io/react-native/docs/tutorial.html.
2. http://www.appcoda.com/react-native-introduction/

Now... let's create a demo movies app.

# Installations
1. `brew install watchman`
2. `npm install -g react-native-cli`

# Set Ups
1. **setting up a sample project** `react-native init MoviesSearch`

# Running the App
Open the newly created project with xCode, then run cmd-R to run the app. if you encounter a red screen with an "Internal Error" please run update your watchman: `brew update` and `brew upgrade watchman`.

You should now have a running node server and an open iOS Simulator running your App's welcome screen!

# Coding
open *index.ios.js* in your favorite IDE.

## Mocking Data
Add mock data for our movies app to work with (until we fetch real data). Our mock data will be in the form of an array of movies, each one containing title, year, and a photos. Add Your mock data to index.ios.js. You can use the following:

`var MOCKED_MOVIES_DATA = [
  {title: 'Boxer', year: '2015', posters: {thumbnail: 'https://upload.wikimedia.org/wikipedia/commons/5/53/Boxer_puppy_fawn_portrai.jpg'}},
];`

## Rendering a Movie
Please refer to React Native's docs to see a list of available components:  https://facebook.github.io/react-native/docs/getting-started.html

Structure your view and css to accommodate the following movie view:
```
+---------------------------------+
|+-------++----------------------+|
||       ||        Title         ||
|| Image ||                      ||
||       ||        Year          ||
|+-------++----------------------+|
+---------------------------------+
```

## Fetching Real Data
We'll fetch data from the following endpoint: 'https://raw.githubusercontent.com/facebook/react-native/master/docs/MoviesExample.json'

The data is structured identically to our mock data.

Make your component statefull, initializing movies with null and loading them on componentDidMount.

To fetch the data you can use the fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
```
fetch(REQUEST_URL)
      .then((response) => response.json())
      .then((responseData) => {
        this.setState({
          movies: responseData.movies,
        });
      })
      .done();
```

## Rendering Real Data
Now modify the render function to render a loading view if we don't have any movies data, and to render the first movie otherwise.

## List View
Let's render a list of movies instead of a single one! We'll use the ListView component to do so.
Why is a ListView better than just rendering all of these elements or putting them in a ScrollView? Despite React being fast, rendering a possibly infinite list of elements could be slow. ListView schedules rendering of views so that you only display the ones on screen and those already rendered but off screen are removed from the native view hierarchy.

1. add ListView to the require list.
2. update the render method to render a ListView if the movies are loaded. Read the Component Docs https://facebook.github.io/react-native/docs/listview.html#content

# Want Some More?
1. Try adding a TabBarIOS to your app. Create a "Featured" tab, and a "Search" tab.

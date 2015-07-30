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

![Image of List]
(http://content.screencast.com/users/shimilid/folders/Jing/media/5fbe3b6d-4dc5-4694-82b3-82a2d8b6b4c0/00000015.png)

1. add ListView to the require list.
2. update the render method to render a ListView if the movies are loaded. Read the Component Docs https://facebook.github.io/react-native/docs/listview.html#content

# Want Some More?
## Adding Tabs
React Native offers a native Tabs component called TabBarIOS. 

![Image of Tabs]
(http://content.screencast.com/users/shimilid/folders/Jing/media/1aad7a87-8a15-4875-83d1-4cd537a9cd79/00000014.png)

1. Copy your implementation to a separate "Featured" module and add a "Search" module.
2. In index.ios.js import the new modules.
3. In index.ios.js clean the unused code and leave a render method that renders a TabBarIOS component with two items. You should render your modules as Directives. Please refer to React Native's Component Docs for implementation details: https://facebook.github.io/react-native/docs/tabbarios.html#content

## Adding Navigator
React Native also offers a native Navigator component that intorudces the native iOS behaviour of a navigation stack allowing navigation to/back from content. The component is called NavigatorIOS. Read More about it here https://facebook.github.io/react-native/docs/navigatorios.html#content.

1. Copy your Featured implementation into a MovieList component.
2. Wrap your single movie render (item in ListView) in a <TouchableHighlight/> component to allow an addition of touch behaviour to it (https://facebook.github.io/react-native/docs/touchablehighlight.html#content) 
3. Update you Featured component to render a NavigatorIOS with an initialRoute of the MovieList 
```             
  <NavigatorIOS
    style={styles.container}
    initialRoute={{
      title: 'Featured Movies',
      component: MovieList
    }}
  />
```
4. Create a MovieDetail component that receives the movie as a prop and renders it somehow
5. Route the MovieList TouchableHighlight onPress to a method that navigates to a movie detail view. A "navigator" prop is passed automatically to the view. Something like this:
```
  <TouchableHighligh onPress="{() => this.showMovieDetail(movie)}"/>
  
  showMovieDetail: function(movie) {
      this.props.navigator.push({
          title: movie.title,
          component: MovieDetail,
          passProps: {movie}
      });
  }
```

*Now watch the MAGIC!*

![Image of Featured]
(http://content.screencast.com/users/shimilid/folders/Jing/media/e439c911-636e-4c18-867c-acf44c67b35b/00000012.png)
![Image of Movie Details]
(http://content.screencast.com/users/shimilid/folders/Jing/media/f199a24f-049a-46f5-952b-0222ec650376/00000013.png)

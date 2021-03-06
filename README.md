# Swift Google Maps API

[![CI Status](https://travis-ci.org/honghaoz/Swift-Google-Maps-API.svg?branch=master)](https://travis-ci.org/honghaoz/Swift-Google-Maps-API)

Use [Google Maps Web Service APIs](https://developers.google.com/maps/get-started/#web-service-apis) in Swift

## Features:
- [x] [Google Maps Directions API](https://developers.google.com/maps/documentation/directions/)
- [ ] [Google Places API Web Service](https://developers.google.com/places/web-service/)
  - [x] [Place Autocomplete](https://developers.google.com/places/web-service/autocomplete)
  - [x] [Place Details](https://developers.google.com/places/web-service/details)
- [ ] More...

## Platforms
- [x] iOS 8.0+
- [x] Mac OS X 10.9+
- [x] watchOS 2.0+
- [x] tvOS 9.0+

## Installation

### [CocoaPods](http://cocoapods.org)
- Google Maps Directions API

  ```ruby
  use_frameworks!
  pod 'GoogleMapsDirections', '~> 1.0'
  ```
- Google Places API

  ```ruby
  use_frameworks!
  pod 'GooglePlaces', '~> 1.0'
  ```
  
## Usage
- Google Maps Directions API
  ```swift
  import GoogleMapsDirections
  
  GoogleMapsDirections.provideAPIKey("A VALID GOOGLE MAPS KEY")
  
  let origin = Place.StringDescription(address: "Davis Center, Waterloo, Canada")
  let destination = Place.StringDescription(address: "Conestoga Mall, Waterloo, Canada")
  
  // You can also use coordinates or placeID for a place
  // let origin = Place.Coordinate(coordinate: LocationCoordinate2D(latitude: 43.4697354, longitude: -80.5397377))
  // let origin = Place.PlaceID(id: "ChIJb9sw59k0K4gRZZlYrnOomfc")
  
  GoogleMapsDirections.direction(fromOrigin: origin, toDestination: destination) { (response, error) -> Void in
    // Check Status Code
    guard response?.status == GoogleMapsDirections.StatusCode.OK else {
      // Status Code is Not OK
      debugPrint(response?.errorMessage)
      return
    }
    
    // Use .result or .geocodedWaypoints to access response details
    // response will have same structure as what Google Maps Directions API returns
    debugPrint("it has \(response?.routes.count ?? 0) routes")
  }
  ```
- Google Places API
  - Place Autocomplete:
    ```swift
    import GooglePlaces
    
    GooglePlaces.provideAPIKey("A VALID GOOGLE MAPS KEY")
    
    GooglePlaces.placeAutocomplete(forInput: "Pub") { (response, error) -> Void in
      // Check Status Code
      guard response?.status == GooglePlaces.StatusCode.OK else {
        // Status Code is Not OK
        debugPrint(response?.errorMessage)
        return
      }
      
      // Use .predictions to access response details
      debugPrint("first matched result: \(response?.predictions.first?.description)")
    }
    
    ```
  - Place Details
    ```swift
    import GooglePlaces
    
    GooglePlaces.provideAPIKey("A VALID GOOGLE MAPS KEY")
    
    GooglePlaces.placeDetails(forPlaceID: "ChIJb9sw59k0K4gRZZlYrnOomfc") { (response, error) -> Void in
      // Check Status Code
      guard response?.status == GooglePlaces.StatusCode.OK else {
        // Status Code is Not OK
        debugPrint(response?.errorMessage)
        return
      }
      
      // Use .result to access response details
      debugPrint("the formated address is: \(response?.result?.formattedAddress)")
    }
    ```

## License

The MIT License (MIT)

Copyright (c) 2015 Honghao Zhang (张宏昊)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

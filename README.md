# TITLE

## Project Links

- [REPO](https://github.com/squirrellypenguin/projectapp)
- [LIVE](https://rg2g.netlify.app/)

## Project Description

Full Stack App which enables users to upload and tag pictures and automagically add gps based on EXIF data.  The uploads are stored and then can me displayed on a dynamic map overlay.  The map overlay will display the user location anda photo locations from the db.  The vision is to allow crowd sourcing of grocery store/donation items similar to [Basket](https://basket.com/).

## Components

### DB
The database will likely have three Models when fully deployed.  

```
  create_table "entry", force: :cascade do |t|
    t.bigint "user_id", null: false
    t.string "name"
    t.string "gps"
    t.string "upc"
    t.integer "price"
    t.string "url"
    t.text :picture_ids, array:true, default: [] 
    t.string "comments"
     t.index ["image_id"], name: "index_facts_on_image_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["user_id"], name: "index_facts_on_user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "password"
    t.string "email"
    t.text :picture_ids, array:true, default: [] 
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end
  
  create_table "image", force: :cascade do |t|
    t.string "name"
    t.string "url"
    t.bigint "user_id", null: false
    t.index ["user_id"], name: "index_facts_on_user_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

```

### Backend

The test environment is Ruby (3.0.1) and Rails (>6).  The backend here will be provide an API that provides CRUD routes to the aforementioned databases.  Furthermore, it will handle some basic image processing.  

The backend needs to receive a POST of an photo.

- Image workflow:
	1. The EXIF data needs to be found. The GEMS that parse these dictionaries are: 
		* [EXIF](https://github.com/tonytonyjan/exif) is the OG.
		* [exiftool.rb](https://github.com/exiftool-rb/exiftool.rb) implmented in pure Ruby.
		* [EXIF Reader]([https://github.com/remvee/exifr) YA-EXIF parser library.
	2. Image Storage:
		* [Cloudinary SDK](https://cloudinary.com/documentation/rails_integration) provides the ability to process and upload the image to this CDN

The backend will also [use JWT](https://dev.to/alexmercedcoder/ruby-on-rails-api-with-jwt-auth-tutorial-go2).  
	
###  Vue.JS Frontend

**App**
```

+-- Header
|   +-- Nav
+-- Main
|   +-- Login 
|       +-- User Record
|       +-- Entry Item CRUD
|   +-- Entry Overall
|   +-- Map View
+-- Footer
```

Right now the core view pages:

| View | Functions |
| --- | ----------- |
| Login | RU |
| User Record | CRUD |
| Landing | R |
| Entry Overall | R|
| Entry Item | CRUD |
| Map view | RU |
| Header | nav |
| Footer | nav |

Additional operability comes from:

- [JWT Auth](https://jwt.io/introduction): Authorization for User
- [GoogleMaps API Marker Clustering](https://developers.google.com/maps/documentation/javascript/marker-clustering): Will allow for the stored gps data on a map
- [Cloudinary](https://cloudinary.com/documentation/): provide  additional image functions
- [GeoLocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API): backup plan for storing GPS database and for getting user location 
	
### Additonal resources for PMVP:
- [Zxing-js](https://dev.to/morinoko/qr-code-reader-on-rails-5816) - UPC JS reader
- [UPC API](https://account.cloudmersive.com/default) - API to process UPC data


## Wireframes
- [Wireframe for functionality and elements](https://www.behance.net/gallery/105110359/ScanBuy-mobile-app?tracking_source=search_projects_recommended%7Cmap%20app)
- [Wireframe fro Desktop UI](https://www.behance.net/gallery/77794611/Find-Vehicle-Inspections-Center?tracking_source=search_projects_recommended%7Cmap%20view%20program%20)
- [Wireframe 1 for mobile style](https://www.behance.net/gallery/117354953/On-demand-service-mobile-app?tracking_source=search_projects_recommended%7Cmap+app)
- [Wireframe 2 for mobile style](https://www.behance.net/gallery/106091453/Parking-App?tracking_source=search_projects_recommended%7Cmap%20app)
- [Wireframe 3 for mobile style](https://www.behance.net/gallery/120271463/Apartment-Search-App-Roomates-Oriented?tracking_source=search_projects_recommended%7Cmap%20app)


## MVP/PostMVP

#### MVP 
- Rails backend with CRUD 
- Vue frontend with CRUD
- Multiple Models
- Image upload  
- Image processing for EXIF
- GPS default location 


| MVP Build Step | Priority | Estimated Time | Actual Time |  |
| --- | :---: |  :---: | :---: | --- |
| Backend Test Build | H | 01 hrs | ∞  | Frame api requests, and request prop handing and state management|
| Backend Test deploy | H | 01 hrs | ∞ | build basic layout for data |
| Frontend Proof of Concept | H | 10 hrs| ∞  | learn new framework |
| Frontend upload handling | H |10 hrs | ∞  | use api/sdk |
| Backend upload handling | H | 10 hrs| ∞  | deal with any image assets basic semantic markup |
| App EXIF processing | M | 05 hrs| ∞  | invoke the library on the file with sane results |
| Frontend GPS user data | M | 10 hrs| ∞  | extract gps from browser |
| Frontend Maps import format | M | 05 hrs| ∞  | format api object for submission |
| Frontend Maps render import | M | 05 hrs| ∞  |  display api results |
| Integrate JWT | M | 10 hrs | ∞ | auth certs!|
| Styling | L | 15 hrs | ∞  | Make viewable and WCAG compliant |
| Code Style | L | 05 hrs | ∞ | 1337 |
| Total | - | 90 hrs |  | |


#### PostMVP 
- Implement Search functionality
- Check if photo is UPC
- Retrieve and store UPC data
- Build out database and relationships


## Code Snippet

```
function reverse(string) {
	// here is the code to reverse a string of text
}
```


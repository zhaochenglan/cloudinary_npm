Cloudinary
==========

Cloudinary is a cloud service that offers a solution to a web application's entire image management pipeline. 

Easily upload images to the cloud. Automatically perform smart image resizing, cropping and conversion without installing any complex software. Integrate Facebook or Twitter profile image extraction in a snap, in any dimension and style to match your website’s graphics requirements. Images are seamlessly delivered through a fast CDN, and much much more. 

Cloudinary offers comprehensive APIs and administration capabilities and is easy to integrate with any web application, existing or new.

Cloudinary provides URL and HTTP based APIs that can be easily integrated with any Web development framework. 

For Node.js, Cloudinary provides an extension for simplifying the integration even further.

## Setup ######################################################################

npm install cloudinary

## Try it right away

Sign up for a [free account](https://cloudinary.com/users/register/free) so you can try out image transformations and seamless image delivery through CDN.

*Note: Replace `demo` in all the following examples with your Cloudinary's `cloud name`.*  

Accessing an uploaded image with the `sample` public ID through a CDN:

    http://res.cloudinary.com/demo/image/upload/sample.jpg

![Sample](https://d3jpl91pxevbkh.cloudfront.net/demo/image/upload/w_0.4/sample.jpg "Sample")

Generating a 150x100 version of the `sample` image and downloading it through a CDN:

    http://res.cloudinary.com/demo/image/upload/w_150,h_100,c_fill/sample.jpg

![Sample 150x100](https://d3jpl91pxevbkh.cloudfront.net/demo/image/upload/w_150,h_100,c_fill/sample.jpg "Sample 150x100")

Converting to a 150x100 PNG with rounded corners of 20 pixels: 

    http://res.cloudinary.com/demo/image/upload/w_150,h_100,c_fill,r_20/sample.png

![Sample 150x150 Rounded PNG](https://d3jpl91pxevbkh.cloudfront.net/demo/image/upload/w_150,h_100,c_fill,r_20/sample.png "Sample 150x150 Rounded PNG")

For plenty more transformation options, see our [image transformations documentation](http://cloudinary.com/documentation/image_transformations).

Generating a 120x90 thumbnail based on automatic face detection of the Facebook profile picture of Bill Clinton:
 
    http://res.cloudinary.com/demo/image/facebook/c_thumb,g_face,h_90,w_120/billclinton.jpg
    
![Facebook 90x120](https://d3jpl91pxevbkh.cloudfront.net/demo/image/facebook/c_thumb,g_face,h_90,w_120/billclinton.jpg "Facebook 90x200")

For more details, see our documentation for embedding [Facebook](http://cloudinary.com/documentation/facebook_profile_pictures) and [Twitter](http://cloudinary.com/documentation/twitter_profile_pictures) profile pictures. 


## Usage

### Configuration

Each request for building a URL of a remote cloud resource must have the `cloud_name` parameter set. 
Each request to our secure APIs (e.g., image uploads, eager sprite generation) must have the `api_key` and `api_secret` parameters set. See [API, URLs and access identifiers](http://cloudinary.com/documentation/api_and_access_identifiers) for more details.

Setting the `cloud_name`, `api_key` and `api_secret` parameters can be done either directly in each call to a Cloudinary method, by calling the cloudinary.config(), or by using the CLOUDINARY_URL environment variable.

### Embedding and transforming images

Any image uploaded to Cloudinary can be transformed and embedded using powerful view helper methods:

The following example generates the url for accessing an uploaded `sample` image while transforming it to fill a 100x150 rectangle:

    cloudinary.url("sample.jpg", {width: 100, height: 150, crop: "fill"})

Another example, emedding a smaller version of an uploaded image while generating a 90x90 face detection based thumbnail: 

    cloudinary.url("woman.jpg", {width: 90, height: 90, crop: "thumb", gravity: "face"})

You can provide either a Facebook name or a numeric ID of a Facebook profile or a fan page.  
             
Embedding a Facebook profile to match your graphic design is very simple:

    cloudinary.url("billclinton.jpg", {width: 90, height: 130, type: "facebook", crop: "fill", gravity: "north_west"})
                           
Same goes for Twitter:

    cloudinary.url("billclinton.jpg", {type: "twitter_name"})

### Upload

Assuming you have your Cloudinary configuration parameters defined (`cloud_name`, `api_key`, `api_secret`), uploading to Cloudinary is very simple.
    
The following example uploads a local JPG to the cloud: 
 
 	var cloudinary = require('cloudinary')
 	   
    cloudinary.uploader.upload("my_picture.jpg", function(result) { console.log(result) })
    
Below is an example of an upload's result:

 	{ public_id: '4srvcynxrf5j87niqcx6w',
 	  version: 1340625837,
 	  signature: '01234567890abcdef01234567890abcdef012345',
 	  width: 200,
 	  height: 200,
 	  format: 'jpg',
 	  resource_type: 'image',
 	  url: 'http://res.cloudinary.com/demo/image/upload/v1340625837/4srvcynxrf5j87niqcx6w.jpg',
 	  secure_url: 'https://d3jpl91pxevbkh.cloudfront.net/demo/image/upload/v1340625837/4srvcynxrf5j87niqcx6w.jpg' } 
        
The uploaded image is assigned a randomly generated public ID. The image is immediately available for download through a CDN:

    cloudinary.url("abcfrmo8zul1mafopawefg.jpg")
        
    http://res.cloudinary.com/demo/image/upload/abcfrmo8zul1mafopawefg.jpg

You can also specify your own public ID:    
    
    cloudinary.uploader.upload("http://www.example.com/image.jpg", function(result) { console.log(result) }, {public_id: 'sample_remote'})

    cloudinary.url("sample_remote.jpg")

    http://res.cloudinary.com/demo/image/upload/sample_remote.jpg
        
### cloudinary.image

Returns an html image tag pointing to Cloudinary.

Usage:

    cloudinary.image("sample", {format: "png", width: 100, height: 100, crop: "fill"})

    // <img src='http://res.cloudinary.com/demo/image/upload/c_fill,h_100,w_100/sample.png' height='100' width='100'/>

## Additional resources ##########################################################

Additional resources are available at:

* [Website](http://cloudinary.com)
* [Documentation](http://cloudinary.com/documentation)
* [Image transformations documentation](http://cloudinary.com/documentation/image_transformations)
* [Upload API documentation](http://cloudinary.com/documentation/upload_images)

## Support

You can [open an issue through GitHub](https://github.com/cloudinary/cloudinary_npm/issues).

Contact us at [info@cloudinary.com](mailto:info@cloudinary.com)

Or via Twitter: [@cloudinary](https://twitter.com/#!/cloudinary)

## License #######################################################################

Released under the MIT license. 

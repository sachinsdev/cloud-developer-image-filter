# Image Filtering Microservice

A Node.js microservice that downloads an image from a public URL, resizes it, converts it to greyscale, and returns the processed image. It validates input, cleans up temporary files after every response, and was deployed to AWS Elastic Beanstalk.

Built in 2020 for Udacity's Cloud Developer nanodegree, as part of the Udagram photo sharing application.

## Tech
* Node.js, Express and TypeScript
* Jimp for image processing
* AWS Elastic Beanstalk for deployment

## API

| Method | Path | Description |
|---|---|---|
| GET | /filteredimage?image_url={url} | Returns the filtered image |
| GET | / | Lists the supported API |

**Responses**
* `200` with the filtered image file
* `400` if `image_url` is missing
* `422` if `image_url` is not a valid URL
* `500` if the image could not be downloaded or processed

**Example**
```
GET /filteredimage?image_url=https://cdn.pixabay.com/photo/2015/02/24/15/41/dog-647528_960_720.jpg
```

## How it works
1. Validates the `image_url` query parameter.
2. Downloads the image with Jimp, resizes it to 256 x 256, converts it to greyscale, and saves it to a temporary file.
3. Streams the result back to the client.
4. Deletes the temporary file once the response is sent, so the service doesn't accumulate files on disk.

## Running it
```
npm install
npm run dev
```
The server runs at http://localhost:8082.

**Deploying to Elastic Beanstalk**
```
npm run build
eb init
eb create
eb deploy
```

A Postman collection (`cloud-cdnd-c2-final.postman_collection.json`) is included, and the [deployment screenshot](deployment_screenshots/udagram-sachin-cloud-dev-dev.png) shows the running environment.

## Note

Uses 2020 era package versions, so dependencies would need updating before deploying today.

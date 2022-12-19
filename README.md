# The-Cat-API
We will enlighten your days with the cutest images of our beloved cats. 
# About # 
Our new API will bring an even better experience to your customers by enlightening their days with the cutest images of their beloved cats :heart:

With this feature, you will be able to do the following:
* upload images;
* search for those images using their IDs or filters;
* delete the images of your choosing.

Our API also provides the smart solution of checking the images before they get uploaded: which means it rejects all images that have no cats in them or any inappropriate content :wink: 

# Authentication # 
* Register at the following address: https://thecatapi.com/signup  
* The key will be sent to the registered email.  

# API path # 
Our call will use the following path: https://api.thecatapi.com/v1

# Images # 
You should follow some requirements in order to upload the images. The parameters are described in the table below. 

Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`id` |Image ID.  | `UUID`| Yes 
`url`| URL to access the image. | `string` | Yes
`width` | Image width in pixels. Automatically generated.| `integer` | Yes 
`height` | Image height in pixels. Automatically generated. | `integer` | Yes 
`sub_id` | ID for internal identification. | `string` | No
`created_at` | Image upload date in format 2022-11-24T17:41:35.000Z | `datetime`  | Yes
`original_filename`| Original file name. | `string` | Yes
`pending` | Internal lifecycle flag. 0=false, 1=true | `integer` | No
`approved` | Internal lifecycle flag. 0=false, 1=true | `integer` | No

# Upload a specific image # 
**Endpoint**: `POST / images/upload`
## Purpose ##
 * Uploads a new image in the system.
 * Accepts .gif, .jpg, or .png files.
 > :warning: The pictures should contain cat images with aproppriate content in order to be accepted. 
 ## Request body ##
 Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`file` |  .gif, .png, ou .jpg file | `file` | Yes 
`sub_id` | ID for internal identification. | `string` | No
## Header parameter ##
Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`x-api_key` | The authentication key received. | `string` | Yes 
## Request sample ## 
``` 
curl --location --request POST 'https://api.thecatapi.com/v1/images/upload' \
--header 'x-api-key: live_n8dNkrkPBQ3ikGoWBN0ghgZgENg2pUlNqQCWQ9T5lxUSN8DymiPWoYOfn5bBDtI9' \
--form 'file=@"mTh90-ez9/supercute.jpg"' \ 
```
## Response sample ## 
``` 
{
    "id": "a-vdC3ydX",
    "url": "https://cdn2.thecatapi.com/images/a-vdC3ydX.jpg",
    "width": 1280,
    "height": 720,
    "original_filename": "supercute.jpg",
    "pending": 0,
    "approved": 1
} 
```
# Get a Specific Image # 
**Endpoint**: `GET / images/{image_id}`
## Purpose ##
* Gets the image corresponding to the `image_id` parameter used as `path` parameter.
## Header parameter ##
Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`x-api_key` | The authentication key received. | `string` | Yes 
## Request sample ## 
```
curl --location --request GET 'https://api.thecatapi.com/v1/images/a-vdC3ydX' \
--header 'x-api-key: live_n8dNkrkPBQ3ikGoWBN0ghgZgENg2pUlNqQCWQ9T5lxUSN8DymiPWoYOfn5bBDtI9'
```
## Response sample ## 
```
{
    "id": "a-vdC3ydX",
    "url": "https://cdn2.thecatapi.com/images/a-vdC3ydX.jpg",
    "width": 1280,
    "height": 720,
}
```
# Get your uploaded images # 
**Endpoint**: `GET / images`
## Purpose ##
* Gets all images uploaded to your account via `/images/upload`. The results can be filtered using the `query` parameters below:

Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`limit` | Number of images to be returned. The maximum value is 25. The default is 1. | `integer` | Yes
`mime_types` | The image types: .gif, .jpg, or .png. Returns all types by default.| `string` delimited by commas | No 
`order`| Return order: RANDOM, ASC, or DESC. The default is RANDOM.| `string`| No
## Header parameter ##
Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`x-api_key` | The authentication key received. | `string` | Yes 
## Request sample ## 
```
curl --location --request GET 'https://api.thecatapi.com/v1/images?limit=10' \
--header 'x-api-key: live_n8dNkrkPBQ3ikGoWBN0ghgZgENg2pUlNqQCWQ9T5lxUSN8DymiPWoYOfn5bBDtI9'
```
## Response sample ## 
```
[
    {
        "breeds": [],
        "id": "a-vdC3ydX",
        "url": "https://cdn2.thecatapi.com/images/a-vdC3ydX.jpg",
        "width": 1280,
        "height": 720,
        "created_at": "2022-12-13T12:36:05.000Z",
        "original_filename": "supercute.jpg",
        "breed_ids": null
    }
]
```
# Delete a specific image # 
**Endpoint**: `DELETE / images/{image_id}`
## Purpose ##
* Deletes the image corresponding to the `image_id` parameter used as `path` parameter.
## Header parameter ##
Name |  Description  | Type  | Required 
:---:| :---: | :---: | :---:
`x-api_key` | The authentication key received. | `string` | Yes 
## Request sample ## 
```
curl --location --request DELETE 'https://api.thecatapi.com/v1/images/UmTtwZPFh' \
--header 'x-api-key: live_n8dNkrkPBQ3ikGoWBN0ghgZgENg2pUlNqQCWQ9T5lxUSN8DymiPWoYOfn5bBDtI9'
```
## Response sample ## 
```
204 no Content
This is a successfull return that indicates the image has been deleted. 
```

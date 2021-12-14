# react-cloudinary-upload-widget

[![NPM](https://img.shields.io/npm/v/react-cloudinary-upload-widget.svg)](https://www.npmjs.com/package/react-cloudinary-upload-widget) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save react-cloudinary-upload-widget
```

## Usage

```jsx
import React from 'react'

import { WidgetLoader, Widget } from 'react-cloudinary-upload-widget'

const Example = () => {
  return (
    <>
      <WidgetLoader /> // add to top of file. Only use once.  
      <Widget
        sources={['local', 'camera', 'dropbox']} // set the sources available for uploading -> by default
        // all sources are available. More information on their use can be found at 
        // https://cloudinary.com/documentation/upload_widget#the_sources_parameter
        sourceKeys={{dropboxAppKey: '1dsf42dl1i2', instagramClientId: 'd7aadf962m'}} // add source keys 
        // and ID's as an object. More information on their use can be found at 
        // https://cloudinary.com/documentation/upload_widget#the_sources_parameter
        resourceType={'image'} // optionally set with 'auto', 'image', 'video' or 'raw' -> default = 'auto'
        cloudName={'example_cloudname'} // your cloudinary account cloud name. 
        // Located on https://cloudinary.com/console/
        uploadPreset={'preset1'} // check that an upload preset exists and check mode is signed or unisgned
        buttonText={'Open'} // default 'Upload Files'
        className={'btn'} // indicate your button class by the class. Default = ''
        style={{
              color: 'white',
              border: 'none',
              width: '120px',
              backgroundColor: 'green',
              borderRadius: '4px',
              height: '25px'
            }} // inline styling only or style id='cloudinary_upload_button'
        folder={'my_folder'} // set cloudinary folder name to send file
        cropping={false} // set ability to crop images -> default = true
        onSuccess={successCallBack} // add success callback -> returns result
        onFailure={failureCallBack} // add failure callback -> returns 'response.error' + 'response.result'
        logging={false} // logs will be provided for success and failure messages, 
        // set to false for production -> default = true
        customPublicId={'sample'} // set a specific custom public_id. 
        // To use the file name as the public_id use 'use_filename={true}' parameter
        eager={'w_400,h_300,c_pad|w_260,h_200,c_crop'} // add eager transformations -> deafult = null
        use_filename={false} // tell Cloudinary to use the original name of the uploaded 
        // file as its public ID -> default = true,

        // 👇 FOR SIGNED UPLOADS ONLY 👇

        generateSignatureUrl={'http://my_domain.com/api/v1/media/generate_signature'} // pass the api 
        // endpoint for generating a signature -> check cloudinary docs and SDK's for signing uploads
        apiKey={00000000000000} // cloudinary API key -> number format
        accepts={'application/json'} // for signed uploads only -> default = 'application/json'
        contentType={'application/json'} // for signed uploads only -> default = 'application/json'
        withCredentials={true} // default = true -> check axios documentation for more information
        unique_filename={true} // setting it to false, you can tell Cloudinary not to attempt to make 
        // the Public ID unique, and just use the normalized file name -> default = true
      />
    </>
  )
}
```

## Example Backend for Signed Uploads (ruby)

example of backend process to create signature for signing uploads to cloudinary. the param 'params_to_sign' will be a json string. Parse this string to create an object/hash. 
Check cloudinary documentation for more information on signing uploads, generating signatures and the various language specific SDK's available for this process. 

This example is from their ruby SDK

```ruby
  def generate_signature
    render json: Cloudinary::Utils.api_sign_request(JSON.parse(params[:params_to_sign]), ENV['CLOUDINARY_SECRET'])
  end
```

## License

MIT © [bubbaspaarx](https://github.com/bubbaspaarx)

---



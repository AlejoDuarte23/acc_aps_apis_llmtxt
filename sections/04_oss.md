## oss

_Generated from `oss.yaml`_

The Object Storage Service (OSS) allows your application to download and upload raw files (such as PDF, XLS, DWG, or RVT) that are managed by the Data service.

---

### List Buckets

**Endpoint:** `GET /oss/v2/buckets`
**Operation ID:** `get_buckets`

#### Description
Returns a list of buckets owned by the application.

#### Parameters
- Ref: `#/components/parameters/region`
- Ref: `#/components/parameters/limit`
- Ref: `#/components/parameters/startAt`

#### Responses
- **200**: The list of buckets was successfully retrieved.

---

### Create Bucket

**Endpoint:** `POST /oss/v2/buckets`
**Operation ID:** `create_bucket`

#### Description
Creates a bucket. 

Buckets are virtual container within the Object Storage Service (OSS), which you can use to store and manage objects (files) in the cloud. The application creating the bucket is the owner of the bucket.

**Note:** Do not use this operation to create buckets for BIM360 Document Management. Use [POST projects/{project_id}/storage](/en/docs/data/v2/reference/http/projects-project_id-storage-POST>) instead. For details, see [Upload Files to BIM 360 Document Management](/en/docs/bim360/v1/tutorials/document-management/upload-document).

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Request Body
- Required: `True`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/create_buckets_payload`

#### Responses
- **200**: Bucket was successfully created.
- **409**: The specified bucket key already exists.

---

### Delete Bucket

**Endpoint:** `DELETE /oss/v2/buckets/{bucketKey}`
**Operation ID:** `delete_bucket`

#### Description
Deletes the specified bucket. Only the application that owns the bucket can call this operation. All other applications that call this operation will receive a "403 Forbidden" error. 

The initial processing of a bucket deletion request can be time-consuming. So, we recommend only deleting buckets containing a few objects, like those typically used for acceptance testing and prototyping. 

**Note:** Bucket keys will not be immediately available for reuse.

#### Parameters
- `bucketKey` in `path` (required: True) — The bucket key of the bucket to delete.

#### Responses
- **200**: The bucket deletion request was accepted.
- **400**: BAD REQUEST, Invalid request due to malformed syntax or missing headers
- **404**: NOT FOUND, The specified ``bucketKey`` does not exist.
- **409**: CONFLICT, The specified bucket is already marked for deletion.

---

### Get Bucket Details

**Endpoint:** `GET /oss/v2/buckets/{bucketKey}/details`
**Operation ID:** `get_bucket_details`

#### Description
Returns detailed information about the specified bucket.

**Note:** Only the application that owns the bucket can call this operation. All other applications that call this operation will receive a "403 Forbidden" error.

#### Parameters
- `bucketKey` in `path` (required: True) — The bucket key of the bucket to query.

#### Responses
- **200**: Bucket details were retrieved successfully.
- **404**: NOT FOUND, Bucket does not exist.

---

### Delete Object

**Endpoint:** `DELETE /oss/v2/buckets/{bucketKey}/objects/{objectKey}`
**Operation ID:** `delete_object`

#### Description
Deletes an object from the bucket.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/objectKey`
- `x-ads-acm-namespace` in `header` (required: False) — This header is used to let the OSS Api Proxy know if ACM is used to authorize access to the given object. If this authorization is used by your service, then you must provide the name of the namespace you want to validate access control policies against.
- `x-ads-acm-check-groups` in `header` (required: False) — Informs the OSS API Proxy know if your service requires ACM authorization to also validate against Oxygen groups. If so, you must pass this header with a value of ``true``. Otherwise, the assumption is that checking authorization against Oxygen groups is not required.
- `x-ads-acm-groups` in `header` (required: False) — Use this header to pass the Oxygen groups you want the OSS Api Proxy to use for group validation for the given user in the OAuth2 token.

#### Responses
- **200**: The object was successfully deleted.
- **404**: NOT FOUND, Bucket does not exist.

---

### List Objects

**Endpoint:** `GET /oss/v2/buckets/{bucketKey}/objects`
**Operation ID:** `get_objects`

#### Description
Returns a list objects in the specified bucket. 

Only the application that owns the bucket can call this operation. All other applications that call this operation will receive a "403 Forbidden" error.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/limit`
- `beginsWith` in `query` (required: False) — Filters the results by the value you specify. Only the objects with their ``objectKey`` beginning with the specified string are returned.
- Ref: `#/components/parameters/startAt`

#### Responses
- **200**: The requested objects were returned successfully

---

### Get Object Details

**Endpoint:** `GET /oss/v2/buckets/{bucketKey}/objects/{objectKey}/details`
**Operation ID:** `get_object_details`

#### Description
Returns detailed information about the specified object.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/objectKey`
- Ref: `#/components/parameters/If-Modified-Since`
- `x-ads-acm-namespace` in `header` (required: False) — This header is used to let the OSS Api Proxy know if ACM is used to authorize access to the given object. If this authorization is used by your service, then you must provide the name of the namespace you want to validate access control policies against.
- `x-ads-acm-check-groups` in `header` (required: False) — Informs the OSS Api Proxy know if your service requires ACM authorization to also validate against Oxygen groups. If so, you must pass this header with a value of ``true``. Otherwise, the assumption is that checking authorization against Oxygen groups is not required.
- `x-ads-acm-groups` in `header` (required: False) — Use this header to pass the Oxygen groups you want the OSS Api Proxy to use for group validation for the given user in the OAuth2 token.
- Ref: `#/components/parameters/with`

#### Responses
- **200**: OK, Get object details was successful.
- **304**: NOT MODIFIED, The supported formats have not been modified since the specified date.
- **404**: NOT FOUND, Object does not exist.

---

### Generate OSS Signed URL

**Endpoint:** `POST /oss/v2/buckets/{bucketKey}/objects/{objectKey}/signed`
**Operation ID:** `create_signed_resource`

#### Description
Generates a signed URL that can be used to download or upload an object within the specified expiration time. If the object the signed URL points to is deleted or expires before the signed URL expires, the signed URL will no longer be valid.

In addition to this operation that generates OSS signed URLs, OSS provides operations to generate S3 signed URLs. S3 signed URLs allow direct upload/download from S3 but are restricted to bucket owners. OSS signed URLs also allow upload/download and can be configured for access by other applications, making them suitable for sharing objects across applications.

Only the application that owns the bucket containing the object can call this operation.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/objectKey`
- Ref: `#/components/parameters/access`
- `useCdn` in `query` (required: False) — ``true`` : Returns a Cloudfront URL to the object instead of an Autodesk URL (one that points to a location on https://developer.api.autodesk.com). Applications can interact with the Cloudfront URL exactly like with any classic public resource in OSS. They can use GET requests to download objects or PUT requests to upload objects.

``false`` : (Default) Returns an Autodesk URL (one that points to a location on https://developer.api.autodesk.com) to the object.

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/create_signed_resource`

#### Responses
- **200**: OK, Success

---

### Download Object Using Signed URL

**Endpoint:** `GET /oss/v2/signedresources/{hash}`
**Operation ID:** `get_signed_resource`

#### Description
Downloads an object using an OSS signed URL.

**Note:** The signed URL returned by [Generate OSS Signed URL](/en/docs/data/v2/reference/http/signedresources-:id-GET/)  contains the ``hash`` URI parameter as well.

#### Parameters
- `Range` in `header` (required: False) — The byte range to download, specified in the form ``bytes=<START_BYTE>-<END_BYTE>``.
- Ref: `#/components/parameters/If-None-Match`
- Ref: `#/components/parameters/If-Modified-Since`
- `Accept-Encoding` in `header` (required: False) — The compression format your prefer to receive the data. Possible values are:

- ``gzip`` - Use the gzip format

**Note:** You cannot use ``Accept-Encoding:gzip`` with a Range header containing an end byte range. OSS will not honor the End byte range if ``Accept-Encoding: gzip`` header is used.
- Ref: `#/components/parameters/region`
- `response-content-disposition` in `query` (required: False) — The value of the Content-Disposition header you want to receive when you download the object using the signed URL. If you do not specify a value, the Content-Disposition header defaults to the value stored with OSS.
- `response-content-type` in `query` (required: False) — The value of the Content-Type header you want to receive when you download the object using the signed URL. If you do not specify a value, the Content-Type header defaults to the value stored with OSS.

#### Responses
- **206**: PARTIAL CONTENT, Partial content of the object is returned as requested.
- **416**: RANGE NOT SATISFIABLE, Request included a Range header that is not valid for this object.

---

### Replace Object Using Signed URL

**Endpoint:** `PUT /oss/v2/signedresources/{hash}`
**Operation ID:** `upload_signed_resource`

#### Description
Replaces an object that already exists on OSS, using an OSS signed URL. 

The signed URL must fulfil the following conditions:

- The signed URL is valid (it has not expired as yet).
- It was generated with ``write`` or ``readwrite`` for the ``access`` parameter.

#### Parameters
- `Content-Type` in `header` (required: False) — The MIME type of the object to upload; can be any type except 'multipart/form-data'. This can be omitted, but we recommend adding it.
- `Content-Length` in `header` (required: True) — The size of the data contained in the request body, in bytes.
- `Content-Disposition` in `header` (required: False) — The suggested file name to use when this object is downloaded as a file.
- Ref: `#/components/parameters/x-ads-region-4-object`
- `If-Match` in `header` (required: False) — The current value of the ``sha1`` attribute of the object you want to replace. OSS checks the ``If-Match`` header against the ``sha1`` attribute of the object in OSS. If they match, OSS allows the object to be overwritten. Otherwise, it means that the object on OSS has been modified since you retrieved the ``sha1`` and the request fails.

#### Request Body
- Required: `True`
- Content-Type: `application/x-www-form-urlencoded`

#### Responses
- **200**: The object was replaced successfully.
- **412**: PRECONDITION FAILED, If the value sent for the `If-Match` header is not equal to the `sha1` value stored in OSS for this object, a Precondition Failed message will be returned.

---

### Delete Object Using Signed URL

**Endpoint:** `DELETE /oss/v2/signedresources/{hash}`
**Operation ID:** `delete_signed_resource`

#### Description
Delete an object using an OSS signed URL to access it.

Only applications that own the bucket containing the object can call this operation.

#### Parameters
- Ref: `#/components/parameters/x-ads-region-4-object`

#### Responses
- **200**: The object was deleted successfully.

---

### Upload Object Using Signed URL

**Endpoint:** `PUT /oss/v2/signedresources/{hash}/resumable`
**Operation ID:** `upload_signed_resources_chunk`

#### Description
Performs a resumable upload using an OSS signed URL. Use this operation to upload an object in chunks.

**Note:** The signed URL returned by [Generate OSS Signed URL](/en/docs/data/v2/reference/http/signedresources-:id-GET/) contains the ``hash`` as a URI parameter.

#### Parameters
- `hash` in `path` (required: True) — The ID component of the signed URL.

**Note:** The signed URL returned by [Generate OSS Signed URL](/en/docs/data/v2/reference/http/signedresources-:id-GET/) contains ``hash`` as a URI parameter.
- `Content-Type` in `header` (required: False) — The MIME type of the object to upload; can be any type except 'multipart/form-data'. This can be omitted, but we recommend adding it.
- `Content-Range` in `header` (required: True) — The byte range to upload, specified in the form ``bytes=<START_BYTE>-<END_BYTE>``.
- `Content-Disposition` in `header` (required: False) — The suggested file name to use when this object is downloaded as a file.
- Ref: `#/components/parameters/x-ads-region-4-object`
- `Session-Id` in `header` (required: True) — An ID to uniquely identify the file upload session.

#### Request Body
- Required: `True`
- Content-Type: `application/x-www-form-urlencoded`

#### Responses
- **200**: Object was uploaded successfully.
- **202**: ACCEPTED, Request accepted but processing not complete. Call this operation iteratively until a 200 is returned.
- **409**: CONFLICT, The specified bucket key already exists.
- **416**: REQUEST RANGE NOT SATISFIABLE, Missing Content-Range header.

---

### Copy Object

**Endpoint:** `PUT /oss/v2/buckets/{bucketKey}/objects/{objectKey}/copyto/{newObjName}`
**Operation ID:** `copyTo`

#### Description
Creates a copy of an object within the bucket.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/objectKey`
- `newObjName` in `path` (required: True) — A URL-encoded human friendly name to identify the copied object.
- `x-ads-acm-namespace` in `header` (required: False) — This header is used to let the OSS Api Proxy know if ACM is used to authorize access to the given object. If this authorization is used by your service, then you must provide the name of the namespace you want to validate access control policies against.
- `x-ads-acm-check-groups` in `header` (required: False) — Informs the OSS Api Proxy know if your service requires ACM authorization to also validate against Oxygen groups. If so, you must pass this header with a value of ``true``. Otherwise, the assumption is that checking authorization against Oxygen groups is not required.
- `x-ads-acm-groups` in `header` (required: False) — Use this header to pass the Oxygen groups you want the OSS Api Proxy to use for group validation for the given user in the OAuth2 token.

#### Responses
- **200**: Object was copied successfully.

---

### Generate Signed S3 Download URL

**Endpoint:** `GET /oss/v2/buckets/{bucketKey}/objects/{objectKey}/signeds3download`
**Operation ID:** `signed_s3_download`

#### Description
Gets a signed URL to download an object directly from S3, bypassing OSS servers. This signed URL expires in 2 minutes by default, but you can change this duration if needed.  You must start the download before the signed URL expires. The download itself can take longer. If the download fails after the validity period of the signed URL has elapsed, you can call this operation again to obtain a fresh signed URL.

Only applications that have read access to the object can call this operation.   

You can use range headers with the signed download URL to download the object in chunks. This ability lets you download chunks in parallel, which can result in faster downloads.

If the object you want to download was uploaded in chunks and is still assembling on OSS, you will receive multiple S3 URLs instead of just one. Each URL will point to a chunk. If you prefer to receive a single URL, set the ``public-resource-fallback`` query parameter to ``true``. This setting will make OSS fallback to returning a single signed OSS URL, if assembling is still in progress. 

In addition to this operation that generates S3 signed URLs, OSS provides an operation to generate OSS signed URLs. S3 signed URLs allow direct upload/download from S3 but are restricted to bucket owners. OSS signed URLs also allow upload/download and can be configured for access by other applications, making them suitable for sharing objects across applications.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- Ref: `#/components/parameters/objectKey`
- `If-None-Match` in `header` (required: False) — The last known ETag value of the object. OSS returns the signed URL only if the ``If-None-Match`` header differs from the ETag value of the object on S3. If not, it returns a 304 "Not Modified" HTTP status.
- `If-Modified-Since` in `header` (required: False) — A timestamp in the HTTP date format (Mon, DD Month YYYY HH:MM:SS GMT). The signed URL is returned only if the object has been modified since the specified timestamp. If not, a 304 (Not Modified) HTTP status is returned.
- `x-ads-acm-scopes` in `header` (required: False) — Optional OSS-compliant scope reference to increase bucket search performance
- `response-content-type` in `query` (required: False) — The value of the Content-Type header you want to receive when you download the object using the signed URL. If you do not specify a value, the Content-Type header defaults to the value stored with OSS.
- `response-content-disposition` in `query` (required: False) — The value of the Content-Disposition header you want to receive when you download the object using the signed URL. If you do not specify a value, the Content-Disposition header defaults to the value stored with OSS.
- `response-cache-control` in `query` (required: False) — The value of the Cache-Control header you want to receive when you download the object using the signed URL. If you do not specify a value, the Cache-Control header defaults to the value stored with OSS.
- `public-resource-fallback` in `query` (required: False) — Specifies how to return the signed URLs, in case the object was uploaded in chunks, and assembling of chunks is not yet complete.

- ``true`` : Return a single signed OSS URL.
- ``false`` : (Default) Return multiple signed S3 URLs, where each URL points to a chunk.
- `minutesExpiration` in `query` (required: False) — The time window (in minutes) the signed URL will remain usable. Acceptable values = 1-60 minutes. Default = 2 minutes.

**Tip:** Use the smallest possible time window to minimize exposure of the signed URL.
- `useCdn` in `query` (required: False) — ``true`` : Returns a URL that points to a CloudFront edge location.

``false`` : (Default) Returns a URL that points directly to the S3 object.
- `redirect` in `query` (required: False) — Generates a HTTP redirection response (Temporary Redirect 307​) using the generated URL.

#### Responses
- **200**: A signed S3 URL was successfully generated.
- **304**: NOT MODIFIED, If-None-Match header matches the object ETag or object has not been modified since the If-Modified-Since date.
- **400**: BAD REQUEST, the request has missing or malformed parameters.
- **401**: UNAUTHORIZED, Invalid authorization header.
- **404**: NOT FOUND, Object or Bucket does not exist.

---

### Batch Generate Signed S3 Upload URLs

**Endpoint:** `POST /oss/v2/buckets/{bucketKey}/objects/batchsigneds3upload`
**Operation ID:** `batch_signed_s3_upload`

#### Description
Creates and returns signed URLs to upload a set of objects directly to S3. These signed URLs expire in 2 minutes by default, but you can change this duration if needed.  You must start uploading the objects before the signed URLs expire. The upload  itself can take longer.

Only the application that owns the bucket can call this operation. All other applications that call this operation will receive a "403 Forbidden" error.

If required, you can request an array of signed URLs for each object, which lets you upload the objects in chunks. Once you upload all chunks you must call the [Complete Batch Upload to S3 Signed URL](/en/docs/data/v2/reference/http/buckets-:bucketKey-objects-:objectKey-batchcompleteupload-POST/) operation to indicate completion. This instructs OSS to assemble the chunks and reconstitute the object on OSS. You must call this operation even if you requested a single signed URL for an object.

If an upload fails after the validity period of a signed URL has elapsed, you can call this operation again to obtain fresh signed URLs. However, you must use the same ``uploadKey`` that was returned when you originally called this operation.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- `useAcceleration` in `query` (required: False) — ``true`` : (Default) Generates a faster S3 signed URL using Transfer Acceleration.

``false``: Generates a standard S3 signed URL.
- `minutesExpiration` in `query` (required: False) — The time window (in minutes) the signed URL will remain usable. Acceptable values = 1-60 minutes. Default = 2 minutes.

**Tip:** Use the smallest possible time window to minimize exposure of the signed URL.

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/batchsigneds3upload_object`

#### Responses
- **200**: The request was successfully processed. The response body will contain objects that indicate the outcome for each object signed URLs were requested for. Objects corresponding to successful request will contain signed URLs. Objects corresponding to failed requests will contain details of the failure.
- **404**: NOT FOUND, Object or Bucket does not exist.

---

### Complete Batch Upload to S3 Signed URLs

**Endpoint:** `POST /oss/v2/buckets/{bucketKey}/objects/batchcompleteupload`
**Operation ID:** `batch_complete_upload`

#### Description
Requests OSS to start reconstituting the set of objects that were uploaded using signed S3 upload URLs. You must call this operation only after all the objects have been uploaded. 

You can specify up to 25 objects in this operation.

#### Parameters
- Ref: `#/components/parameters/bucketKey`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/batchcompleteupload_object`

#### Responses
- **200**: The request was successfully processed. The response body will contain objects that indicate the outcome for each uploaded object.
- **404**: Object or Bucket does not exist.

---

### Batch Generate Signed S3 Download URLs

**Endpoint:** `POST /oss/v2/buckets/{bucketKey}/objects/batchsigneds3download`
**Operation ID:** `batch_signed_s3_download`

#### Description
Creates and returns signed URLs to download a set of objects directly from S3. These signed URLs expire in 2 minutes by default, but you can change this duration if needed.  You must start download the objects before the signed URLs expire. The download itself can take longer.

Only the application that owns the bucket can call this operation. All other applications that call this operation will receive a "403 Forbidden" error.

#### Parameters
- Ref: `#/components/parameters/bucketKey`
- `public-resource-fallback` in `query` (required: False) — Specifies how to return the signed URLs, in case the object was uploaded in chunks, and assembling of chunks is not yet complete.

- ``true`` : Return a single signed OSS URL.
- ``false`` : (Default) Return multiple signed S3 URLs, where each URL points to a chunk.
- `minutesExpiration` in `query` (required: False) — The time window (in minutes) the signed URL will remain usable. Acceptable values = 1-60 minutes. Default = 2 minutes.

**Tip:** Use the smallest possible time window to minimize exposure of the signed URL.

#### Request Body
- Required: `True`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/batchsigneds3download_object`

#### Responses
- **200**: The request was successfully processed. The response body will contain objects that indicate the outcome for each object signed URLs were requested for. Objects corresponding to successful request will contain signed URLs. Objects corresponding to failed requests will contain details of the failure.
- **400**: BAD REQUEST, the request has missing or malformed parameters.
- **404**: NOT FOUND, Object or Bucket does not exist.

---

### Generate Signed S3 Upload URL

**Endpoint:** `GET /oss/v2/buckets/{bucketKey}/objects/{objectKey}/signeds3upload`
**Operation ID:** `signed_s3_upload`

#### Description
Gets a signed URL to upload an object directly to S3, bypassing OSS servers. You can also request an array of signed URLs which lets you upload an object in chunks.

This signed URL expires in 2 minutes by default, but you can change this duration if needed.  You must start the upload before the signed URL expires. The upload itself can take longer. If the upload fails after the validity period of the signed URL has elapsed, you can call this operation again to obtain a fresh signed URL (or an array of signed URLs as the case may be). However, you must use the same ``uploadKey`` that was returned when you originally called this operation. 

Only applications that own the bucket can call this operation.

**Note:** Once you upload all chunks you must call the [Complete Upload to S3 Signed URL](/en/docs/data/v2/reference/http/buckets-:bucketKey-objects-:objectKey-signeds3upload-POST/) operation to indicate completion. This instructs OSS to assemble the chunks and reconstitute the object on OSS. You must call this operation even when using a single signed URL. 

In addition to this operation that generates S3 signed URLs, OSS provides an operation to generate OSS signed URLs. S3 signed URLs allow direct upload/download from S3 but are restricted to bucket owners. OSS signed URLs also allow upload/download and can be configured for access by other applications, making them suitable for sharing objects across applications.

#### Parameters
- `x-ads-acm-scopes` in `header` (required: False) — Optional OSS-compliant scope reference to increase bucket search performance
- `parts` in `query` (required: False) — The number of parts you intend to chunk the object for uploading. OSS will return that many signed URLs, one URL for each chunk. If you do not specify a value you'll get only one URL to upload the entire object.
- `firstPart` in `query` (required: False) — The index of the first chunk to be uploaded.
- `uploadKey` in `query` (required: False) — The ``uploadKey`` of a previously-initiated upload, in order to request more chunk upload URLs for the same upload. If you do not specify a value, OSS will initiate a new upload entirely.
- `minutesExpiration` in `query` (required: False) — The time window (in minutes) the signed URL will remain usable. Acceptable values = 1-60 minutes. Default = 2 minutes.

**Tip:** Use the smallest possible time window to minimize exposure of the signed URL.
- `useAcceleration` in `query` (required: False) — ``true`` : (Default) Generates a faster S3 signed URL using Transfer Acceleration.

``false``: Generates a standard S3 signed URL.

#### Responses
- **200**: Signed URLs were successfully generated.
- **404**: NOT FOUND, Bucket does not exist.

---

### Complete Upload to S3 Signed URL

**Endpoint:** `POST /oss/v2/buckets/{bucketKey}/objects/{objectKey}/signeds3upload`
**Operation ID:** `complete_signed_s3_upload`

#### Description
Requests OSS to assemble and reconstitute the object that was uploaded using signed S3 upload URL. You must call this operation only after all parts/chunks of the object has been uploaded.

#### Parameters
- `Content-Type` in `header` (required: True) — Must be ``application/json``.
- `x-ads-meta-Content-Type` in `header` (required: False) — The Content-Type value for the uploaded object to record within OSS.
- `x-ads-meta-Content-Disposition` in `header` (required: False) — The Content-Disposition value for the uploaded object to record within OSS.
- `x-ads-meta-Content-Encoding` in `header` (required: False) — The Content-Encoding value for the uploaded object to record within OSS.
- `x-ads-meta-Cache-Control` in `header` (required: False) — The Cache-Control value for the uploaded object to record within OSS.
- `x-ads-user-defined-metadata` in `header` (required: False) — Custom metadata to be stored with the object, which can be retrieved later on download or when retrieving object details. Must be a JSON object that is less than 100 bytes.

#### Request Body
- Required: `True`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/completes3upload_body`

#### Responses
- **200**: Upload successfully completed
- **404**: NOT FOUND, Object or Bucket does not exist.

---


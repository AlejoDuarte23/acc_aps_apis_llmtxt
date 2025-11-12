## Model Derivative

_Generated from `modelderivative.yaml`_

Use the Model Derivative API to translate designs from one CAD format to another.

---

### List Supported Formats

**Endpoint:** `GET /modelderivative/v2/designdata/formats`
**Operation ID:** `get-formats`

#### Description
Returns an up-to-date list of supported translations. It lets you determine the types of derivatives supported for each source design file type. Furthermore, you can get it to retrieve only the translations that have been updated since a date you specify.

See the `Supported Translation Formats table </en/docs/model-derivative/v2/overview/supported-translations>`_ for more details.

**Note:** We keep adding new file formats to our supported translations list, constantly.

#### Parameters
- `If-Modified-Since` in `header` (required: False) — Specifies a date in the ``Day of the week, DD Month YYYY HH:MM:SS GMT`` format. The response will contain only the formats modified since the specified date and time. If you specify an invalid date, the response will contain all supported formats. If no changes have been made after the specified date, the service returns HTTP status ``304``, NOT MODIFIED.
- Ref: `#/components/parameters/accept-encoding`

#### Responses
- **200**: A list of supported formats was successfully returned.
- **304**: Supported formats have not changed since the date specified by the ``If-Modified-Since`` header.

---

### List Model Views

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/metadata`
**Operation ID:** `get-model-views`

#### Description
Returns a list of Model Views (Viewables) in the source design specified by the ``urn`` parameter. It also returns an ID that uniquely identifies the Model View. You can use these IDs with other metadata operations to obtain information about the objects within those Model Views.

Designs created with applications like Fusion 360 and Inventor contain only one Model View per design. Applications like Revit allow multiple Model Views per design.

**Note:** You can retrieve metadata only from a design that has already been translated to SVF or SVF2.

#### Parameters
- Ref: `#/components/parameters/accept-encoding`

#### Responses
- **200**: Success

---

### Fetch Object tree

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/metadata/{modelGuid}`
**Operation ID:** `get-object-tree`

#### Description
Retrieves the structured hierarchy of objects, known as an object tree, from the specified Model View (Viewable) within the specified source design. The object tree represents the arrangement and relationships of various objects present in that Model View.

**Note:** A design file must be translated to SVF or SVF2 before you can retrieve its object tree.  

Before you call this operation:

- Use the `List Model Views </en/docs/model-derivative/v2/reference/http/metadata/urn-metadata-GET/>`_ operation to obtain the list of Model Views in the source design.
- Pick the ID of the Model View you want to query and specify that ID as the value for the ``modelGuid``  parameter.

#### Parameters
- Ref: `#/components/parameters/accept-encoding`
- Ref: `#/components/parameters/x-ads-force`
- Ref: `#/components/parameters/x-ads-derivative-format`
- Ref: `#/components/parameters/forceget`
- `objectid` in `query` (required: False) — If specified, retrieves the sub-tree that has the specified object ID as its parent node. If this parameter is not specified, retrieves the entire object tree.
- `level` in `query` (required: False) — Specifies how many child levels of the hierarchy to return, when the ``objectid``  parameter is specified. Currently supports only ``level`` = ``1``.

#### Responses
- **200**: Success
- **202**: Request accepted but processing not complete. Call this operation iteratively until a 200 is returned.

---

### Fetch All Properties

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/metadata/{modelGuid}/properties`
**Operation ID:** `get-all-properties`

#### Description
Returns a list of properties of all objects in the  Model View specified by the ``modelGuid`` parameter. 

This operation returns properties of all objects by default. However, you can restrict the results to a specific object by specifying its ID as the ``objectid`` parameter.

Properties are returned as a flat list, ordered, by their ``objectid``. The ``objectid`` is a non-persistent ID assigned to an object when the source design is translated to the SVF or SVF2 format. This means that:

- A design file must be translated to SVF or SVF2 before you can retrieve properties.
- The ``objectid`` of an object can change if the design is translated to SVF or SVF2 again. If you require a persistent ID across translations, use ``externalId`` to reference objects, instead of ``objectid``.

Before you call this operation:

- Use the `List Model Views </en/docs/model-derivative/v2/reference/http/metadata/urn-metadata-GET/>`_ operation to obtain the list of Model Views (Viewables) in the source design. 
- Pick the ID of the Model View you want to query and specify that ID as the value for the ``modelGuid`` parameter.

**Tip**: Use `Fetch Specific Properties </en/docs/model-derivative/v2/reference/http/metadata/urn-metadata-guid-properties-GET/>`_ to retrieve only the objects and properties of interest. What’s more, the response is paginated. So, when the number of properties returned is large, responses start arriving more promptly.

#### Parameters
- Ref: `#/components/parameters/accept-encoding`
- Ref: `#/components/parameters/x-ads-force`
- Ref: `#/components/parameters/x-ads-derivative-format`
- `objectid` in `query` (required: False) — The Object ID of the object you want to restrict the response to. If you do not specify this parameter, all properties of all objects within the Model View are returned.
- Ref: `#/components/parameters/forceget`

#### Responses
- **200**: Success.
- **202**: Request accepted but processing not complete. Call this operation again, until you recieve 200 OK.

---

### Fetch Specific Properties

**Endpoint:** `POST /modelderivative/v2/designdata/{urn}/metadata/{modelGuid}/properties:query`
**Operation ID:** `fetch-specific-properties`

#### Description
Queries the objects in the Model View (Viewable) specified by the ``modelGuid`` parameter and returns the specified properties in a paginated list. You can limit the number of objects to be queried by specifying a filter using the ``query`` attribute in the request body.

**Note:** A design file must be translated to SVF or SVF2 before you can query object properties.  

Before you call this operation:

- Use the `List Model Views </en/docs/model-derivative/v2/reference/http/metadata/urn-metadata-GET/>`_ operation to obtain the list of Model Views in the source design.
- Pick the ID of the Model View you want to query and specify that ID as the value for the ``modelGuid``  parameter.

#### Parameters
- Ref: `#/components/parameters/accept-encoding`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/SpecificPropertiesPayload`

#### Responses
- **200**: Success
- **202**: Request accepted but processing is not complete. Call this operation again, until you receive 200 OK.

---

### Fetch Thumbnail

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/thumbnail`
**Operation ID:** `get-thumbnail`

#### Description
Downloads a thumbnail of the specified source design.

#### Parameters
- `width` in `query` (required: False) — Width of thumbnail.  

Possible values: 100, 200, 400  

If ``width`` is omitted, but ``height`` is specified, ``width`` defaults to ``height``. If both ``width`` and ``height`` are omitted, the server will return a thumbnail closest to 200, if such a thumbnail is available.
- `height` in `query` (required: False) — Height of thumbnails.

Possible values: ``100``, ``200``, ``400``.

If ``height`` is omitted, but ``width`` is specified, ``height`` defaults to ``width``.  If both ``width`` and ``height`` are omitted, the server will return a thumbnail closest to 200, if such a thumbnail is available.

#### Responses
- **200**: Success

---

### Fetch Derivative Download URL

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/manifest/{derivativeUrn}/signedcookies`
**Operation ID:** `get-derivative-url`

#### Description
Returns a download URL and a set of signed cookies, which lets you securely download the derivative specified by the `derivativeUrn` URI parameter. The signed cookies have a lifetime of 6 hours. Although you cannot use range headers for this operation, you can use range headers for the returned download URL to download the derivative in chunks, in parallel.

#### Parameters
- `minutes-expiration` in `query` (required: False) — Specifies how many minutes the signed cookies should remain valid. Default value is 360 minutes. The value you specify must be lower than the default value for this parameter. If you specify a value greater than the default value, the Model Derivative service will return an error with an HTTP status code of 400.
- `response-content-disposition` in `query` (required: False) — The value that must be returned with the download URL as the ``response-content-disposition`` query string parameter. Must begin with ``attachment``. This value defaults to the default value corresponding to the derivative/file.

#### Responses
- **200**: Success

---

### Check Derivative Details

**Endpoint:** `HEAD /modelderivative/v2/designdata/{urn}/manifest/{derivativeUrn}`
**Operation ID:** `head-check-derivative`

#### Description
Returns information about the specified derivative.

This operation returns a set of headers similar to that returned by `Download Derivative </en/docs/model-derivative/v2/reference/urn-manifest-derivativeurn-GET>`_.

You can use this operation to determine the total content length of a derivative before you download it. If the derivative is large, you can choose to download the derivative in chunks, by specifying a chunk size using the Range header parameter.

#### Responses
- **200**: Success
- **202**: Request accepted but processing not complete. Call this operation again, until getting 200 OK.

---

### Fetch Manifest

**Endpoint:** `GET /modelderivative/v2/designdata/{urn}/manifest`
**Operation ID:** `get-manifest`

#### Description
Retrieves the manifest of the specified source design.

The manifest is a JSON file containing information about all the derivatives translated from the specified source design. It contains information such as the URNs of the derivatives, the translation status of each derivative, and much more.

The first time you translate a source design, the Model Derivative service creates a manifest for that source design. Thereafter, every time you translate that source design, even to a different format, the Model Derivative service updates that manifest. It does not create a new manifest. Instead, it keeps track of all derivatives of that design.  

When the Model Derivative service starts a translation job (as a result of a request you make using `Submit Translation Job </en/docs/model-derivative/v2/reference/http/jobs/job-POST/>`_), it keeps on updating the manifest at regular intervals. So, you can use the manifest to check the status and progress of each derivative that is being generated. When multiple derivatives have been requested each derivative may complete at a different time. So, each derivative has its own ``status`` attribute. The manifest also contains an overall ``status`` attribute. The overall ``status`` becomes ``complete`` when the ``status`` of all individual derivatives become complete.

Once the translation status of a derivative is ``complete`` you can download the URN.

**Note**: You cannot download 3D SVF2 derivatives.

#### Parameters
- Ref: `#/components/parameters/accept-encoding`

#### Responses
- **200**: Success

---

### Delete Manifest

**Endpoint:** `DELETE /modelderivative/v2/designdata/{urn}/manifest`
**Operation ID:** `delete-manifest`

#### Description
Deletes the manifest of the specified source design. It also deletes all derivatives (translated output files) generated from the source design. However, it does not delete the source design.

**Note:** This operation is idempotent. So, if you call it multiple times, even when no manifest exists, will still return a successful response (200).

#### Responses
- **200**: Success.

---

### Submit Translation Job

**Endpoint:** `POST /modelderivative/v2/designdata/job`
**Operation ID:** `start-job`

#### Description
Creates a job to translate the specified source design to another format, generating derivatives of the source design. You can optionaly:

- Extract selected parts of a design and export the set of geometries in OBJ format.
- Generate different-sized thumbnails.

When the translation job runs, progress information and details of the generated derivatives are logged to a JSON file that is called a manifest. A manifest is typically created the first time you translate the source design. Thereafter the system updates the same manifest each time a translation job is executed for that source design. If necessary, you can set the ``x-ads-force`` parameter to ``true``, which deletes the existing manifest and creates a fresh manifest. However, if you do so, all derivatives generated prior to this are deleted.

#### Parameters
- Ref: `#/components/parameters/x-ads-force`
- Ref: `#/components/parameters/x-ads-derivative-format`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/JobPayload`

#### Responses
- **200**: Success
- **201**: The requested file type has been previously generated and has not been replaced by the new source file.

---

### Specify References

**Endpoint:** `POST /modelderivative/v2/designdata/{urn}/references`
**Operation ID:** `specify-references`

#### Description
Specifies the location of the files referenced by the specified source design.

If a source design contains references to other files, you must set  ``checkReferences`` to ``true``, when you call `Submit Translation Job </en/docs/model-derivative/v2/reference/http/job-POST>`_.  The Model Derivative service will then use the details you specify in this operation to locate and download the referenced files.

#### Request Body
- Required: `False`
- Content-Type: `application/json`

#### Responses
- **200**: Success

---


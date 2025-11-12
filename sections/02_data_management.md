## Data Management API

_Generated from `datamanagement.yaml`_

The Data Management API provides a unified and consistent way to access data across BIM 360 Team, Fusion Team (formerly known as A360 Team), BIM 360 Docs, A360 Personal, and the Object Storage Service.

With this API, you can accomplish a number of workflows, including accessing a Fusion model in Fusion Team and getting an ordered structure of items, IDs, and properties for generating a bill of materials in a 3rd-party process. Or, you might want to superimpose a Fusion model and a building model to use in the Viewer.

---

### List Hubs

**Endpoint:** `GET /project/v1/hubs`
**Operation ID:** `getHubs`

#### Description
Returns a collection of hubs that the user of your app can access.

The returned hubs can be BIM 360 Team hubs, Fusion Team hubs (formerly known as A360 Team hubs), A360 Personal hubs, ACC Docs (Autodesk Docs) accounts, or BIM 360 Docs accounts. Only active hubs are returned.

For BIM 360 Docs and ACC Docs, a hub ID corresponds to an Account ID. To convert a BIM 360 or ACC Account ID to a hub ID, prefix the Account ID with ``b.``. For example, an Account ID of ```c8b0c73d-3ae9``` translates to a hub ID of ``b.c8b0c73d-3ae9``.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_name`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of hubs was successfully retrieved.

---

### Get a Hub

**Endpoint:** `GET /project/v1/hubs/{hub_id}`
**Operation ID:** `getHub`

#### Description
Returns the hub specified by the ``hub_id`` parameter.

For BIM 360 Docs, a hub ID corresponds to a BIM 360 account ID. To convert a BIM 360 account ID to a hub ID, prefix the account ID with ``b.``. For example, an account ID of ```c8b0c73d-3ae9``` translates to a hub ID of ``b.c8b0c73d-3ae9``.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The hub was successfully retrieved.

---

### Get Projects

**Endpoint:** `GET /project/v1/hubs/{hub_id}/projects`
**Operation ID:** `getHubProjects`

#### Description
Returns a collection of active projects within the specified hub. The returned projects can be Autodesk Construction Cloud (ACC), BIM 360, BIM 360 Team, Fusion Team, and A360 Personal projects. 

For BIM 360 and ACC projects a hub ID corresponds to an Account ID. To convert an Account ID to a hub ID, prefix the account ID with ``b.``. For example, a BIM 360 account ID of ```c8b0c73d-3ae9``` translates to a hub ID of ``b.c8b0c73d-3ae9``.

Similarly, to convert a BIM 360 and ACC project IDs to  Data Management project IDs prefix the BIM 360 or ACC Project ID with ``b.``. For example, a project ID of ``c8b0c73d-3ae9`` translates to a project ID of ``b.c8b0c73d-3ae9``.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`
- Ref: `#/components/parameters/page_number`
- Ref: `#/components/parameters/page_limit`

#### Responses
- **200**: The list of projects was successfully retrieved.

---

### Get a Project

**Endpoint:** `GET /project/v1/hubs/{hub_id}/projects/{project_id}`
**Operation ID:** `getProject`

#### Description
Returns the specified project from within the specified hub.

For BIM 360 Docs, a hub ID corresponds to a BIM 360 account ID. To convert a BIM 360 account ID to a hub ID, prefix the account ID with ``b.``. For example, an account ID of ```c8b0c73d-3ae9``` translates to a hub ID of ``b.c8b0c73d-3ae9``.

Similarly, to convert a BIM 360 project ID to a Data Management project ID prefix the BIM 360 Project ID with ``b.``. For example, a project ID of ``c8b0c73d-3ae9`` translates to a project ID of ``b.c8b0c73d-3ae9``.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The project was successfully retrieved.

---

### Get Hub for Project

**Endpoint:** `GET /project/v1/hubs/{hub_id}/projects/{project_id}/hub`
**Operation ID:** `getProjectHub`

#### Description
Returns the hub that contains the project specified by the  ``project_id`` parameter.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: Information about the hub was successfully returned.

---

### List Top-level Project Folders

**Endpoint:** `GET /project/v1/hubs/{hub_id}/projects/{project_id}/topFolders`
**Operation ID:** `getProjectTopFolders`

#### Description
Returns the details of the highest level folders within a project that the user calling this operation has access to. The user must have at least read access to the folders.

If the user is a Project Admin, it returns all top-level folders in the project. Otherwise, it returns all the highest level folders in the folder hierarchy the user has access to.

Users with access permission to a folder has access permission to all its subfolders.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/excludeDeleted`
- Ref: `#/components/parameters/projectFilesOnly`

#### Responses
- **200**: The top-level folders of the specified project were returned successfully.

---

### Get a Folder

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}`
**Operation ID:** `getFolder`

#### Description
Returns the folder specified by the ``folder_id`` parameter from within the project identified by the ``project_id`` parameter. All folders and subfolders within a project (including the root folder) have a unique ID.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/If-Modified-Since`
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The specified folder was successfully retrieved.

---

### Modify a Folder

**Endpoint:** `PATCH /data/v1/projects/{project_id}/folders/{folder_id}`
**Operation ID:** `patchFolder`

#### Description
Renames, moves, hides, or unhides a folder. Marking a BIM 360 Docs folder as hidden effectively deletes it. You can restore it by changing its ``hidden`` attribute. You can also move BIM 360 Docs folders by changing their parent folder.

You cannot permanently delete BIM 360 Docs folders. They are tagged as hidden folders and are removed from the BIM 360 Docs UI and from regular Data Management API responses. You can use the hidden filter (``filter[hidden]=true``) to get a list of deleted folders with the [List Folder Contents](/en/docs/data/v2/reference/http/projects-project_id-folders-folder_id-contents-GET/) operation.

Before you use the Data Management API to access BIM 360 Docs folders, provision your app through the BIM 360 Account Administrator portal. For details, see the [Manage Access to Docs tutorial](/en/docs/bim360/v1/tutorials/getting-started/manage-access-to-docs/).

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](/en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/ModifyFolder`

#### Responses
- **200**: The folder was successfully modified.

---

### Get Parent of a Folder

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/parent`
**Operation ID:** `getFolderParent`

#### Description
Returns the parent folder of the specified folder. In a project, folders are organized in a hierarchy. Each folder except for the root folder has a parent folder.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The parent folder was retrieved successfully.

---

### List Folder Contents

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/contents`
**Operation ID:** `getFolderContents`

#### Description
Returns a list of items and folders within the specified folder. Items represent word documents, fusion design files, drawings, spreadsheets, etc.

The resources contained in the ``included`` array of the response are their tip versions.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`
- Ref: `#/components/parameters/filter_lastModifiedTimeRollup`
- Ref: `#/components/parameters/page_number`
- Ref: `#/components/parameters/page_limit`
- Ref: `#/components/parameters/includeHidden`

#### Responses
- **200**: The content of the specified folder was successfully returned.

---

### List Related Resources for a Folder

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/refs`
**Operation ID:** `getFolderRefs`

#### Description
Returns the resources (items, folders, and versions) that have a custom relationship with the specified folder. Custom relationships can be established between a folder and other resources within the data domain service (folders, items, and versions).

Each relationship is defined by the id of the object at the other end of the relationship, together with type, attributes, and relationships links.
Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of related resources was retrieved successfully.

---

### List Folder and Subfolder Contents

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/search`
**Operation ID:** `getFolderSearch`

#### Description
Searches the specified folder and its subfolders and returns a list of the latest versions of the items you can access.


Use the ``filter`` query string parameter to narrow down the list as appropriate. You can filter by the following properties of the version payload: 

- ``type`` property, 
- ``id`` property, 
- any of the attributes object properties. 

For example, you can filter by ``createTime`` and ``mimeType``. It returns tip versions (latest versions) of properties where the filter conditions are satisfied. To verify the properties of the attributes object for a specific version, use the [Get a Version](/en/docs/data/v2/reference/http/projects-project_id-versions-version_id-GET/) operation.

To list the immediate contents of the folder without parsing subfolders, use the [List Folder Contents](/en/docs/data/v2/reference/http/projects-project_id-folders-folder_id-contents-GET/) operation.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/filter`
- Ref: `#/components/parameters/page_number`

#### Responses
- **200**: The contents of the folder and its subfolders were successfully returned.

---

### List Custom Relationships for a Folder

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/relationships/refs`
**Operation ID:** `getFolderRelationshipsRefs`

#### Description
Returns the custom relationships associated with the specified folder. Custom relationships can be established between a folder and other resources within the data domain service (folders, items, and versions).

Each relationship is defined by the ID of the object at the other end of the relationship, together with type, specific reference meta including extension data.
Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.
The response body will have an included array that contains the resources in the relationship, which is essentially what is returned by the [List Related Resources for a Folder](/en/docs/data/v2/reference/http/projects-project_id-folders-folder_id-refs-GET/) operation.  

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_refType`
- Ref: `#/components/parameters/filter_direction`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of custom relationships was successfully retrieved.

---

### Create a Custom Relationship for a Folder

**Endpoint:** `POST /data/v1/projects/{project_id}/folders/{folder_id}/relationships/refs`
**Operation ID:** `postFolderRelationshipsRef`

#### Description
Creates a custom relationship between a folder and another resource within the data domain service (folder, item, or version).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/RelationshipRefsRequest`

#### Responses
- **204**: The reference between resources was successfully created.

---

### List Relationship Links for a Folder

**Endpoint:** `GET /data/v1/projects/{project_id}/folders/{folder_id}/relationships/links`
**Operation ID:** `getFolderRelationshipsLinks`

#### Description
Returns a list of links for the specified folder. 

Custom relationships can be established between a folder and other external resources residing outside the data domain service. A link’s ``href`` attribute defines the target URI to access a resource.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: Successful retrieval of the links collection associated with a specific resource.

---

### Get an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}`
**Operation ID:** `getItem`

#### Description
Retrieves an item. Items represent Word documents, Fusion 360 design files, drawings, spreadsheets, etc.

The tip version for the item is included in the included array of the payload.
To retrieve multiple items, see the ListItems command.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/includePathInProject`

#### Responses
- **200**: The specified item was retrieved successfully.

---

### Update an Item

**Endpoint:** `PATCH /data/v1/projects/{project_id}/items/{item_id}`
**Operation ID:** `patchItem`

#### Description
Updates the ``displayName`` of the specified item. Note that updating the ``displayName`` of an item is not supported for BIM 360 Docs or ACC items.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/ItemRequest`

#### Responses
- **200**: Updated the item’s properties successfully.

---

### Get Parent of an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/parent`
**Operation ID:** `getItemParentFolder`

#### Description
Returns the parent folder of the specified item.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The parent folder was retrieved successfully.

---

### List Custom Relationships for an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/relationships/refs`
**Operation ID:** `getItemRelationshipsRefs`

#### Description
Returns the custom relationships that are associated with the specified item. Custom relationships can be established between an item and other resources within the ``data`` domain service (folders, items, and versions).

Each relationship is defined by the ID of the object at the other end of the relationship, together with type, specific reference meta including extension data.
Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.
The response body will have an included array that contains the resources in the relationship, which is essentially what is returned by the [List Related Resources for an Item](/en/docs/data/v2/reference/http/projects-project_id-items-item_id-refs-GET/) operation.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_refType`
- Ref: `#/components/parameters/filter_direction`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of custom relationships was successfully retrieved.

---

### Create a Custom Relationship for an Item

**Endpoint:** `POST /data/v1/projects/{project_id}/items/{item_id}/relationships/refs`
**Operation ID:** `postItemRelationshipsRef`

#### Description
Creates a custom relationship between an item and another resource within the data domain service (folder, item, or version).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/RelationshipRefsRequest`

#### Responses
- **204**: A custom relationship for the item was successfully created.

---

### List Related Resources for an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/refs`
**Operation ID:** `getItemRefs`

#### Description
Returns the resources (items, folders, and versions) that have a custom relationship with the specified item. Custom relationships can be established between an item and other resources within the data domain service (folders, items, and versions).


Each relationship is defined by the ID of the object at the other end of the relationship, together with type, attributes, and relationships links.
Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.


**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of related resources was successfully retrieved.
- **403**: Forbidden

---

### List Relationship Links for an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/relationships/links`
**Operation ID:** `getItemRelationshipsLinks`

#### Description
Returns a list of links for the specified item. 

Custom relationships can be established between an item and other external resources residing outside the data domain service. A link’s ``href`` attribute defines the target URI to access a resource.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The relationship links for the item were retrieved successfully.

---

### Get Tip Version of an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/tip`
**Operation ID:** `getItemTip`

#### Description
Returns the latest version of the specified item. A project can contain multiple versions of a resource item. The latest version is referred to as the tip version, which is returned by this operation.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The tip version of the item was retrieved successfully.

---

### List all Versions of an Item

**Endpoint:** `GET /data/v1/projects/{project_id}/items/{item_id}/versions`
**Operation ID:** `getItemVersions`

#### Description
Lists all versions of the specified item. A project can contain multiple versions of a resource item.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`
- Ref: `#/components/parameters/filter_versionNumber`
- Ref: `#/components/parameters/page_number`
- Ref: `#/components/parameters/page_limit`

#### Responses
- **200**: All versions of the specified item were successfully retrieved.

---

### Get a Version

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}`
**Operation ID:** `getVersion`

#### Description
Returns the specified version of an item.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The specified version was retrieved successfully.

---

### Update a Version

**Endpoint:** `PATCH /data/v1/projects/{project_id}/versions/{version_id}`
**Operation ID:** `patchVersion`

#### Description
Updates the properties of the specified version of an  item. Currently, you can only change the name of the version.

**Note:** This operation is not supported for BIM 360 and ACC. If you want to rename a version, create a new version with a new name.

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/VersionRequest`

#### Responses
- **200**: The version was updated successfully.

---

### Get Item by Version

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}/item`
**Operation ID:** `getVersionItem`

#### Description
Returns the item corresponding to the specified version.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: Successful retrieval of a specific item.

---

### List Related Resources for a Version

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}/refs`
**Operation ID:** `getVersionRefs`

#### Description
Returns the resources (items, folders, and versions) that have a custom relationship with the specified version.

Custom relationships can be established between a version of an item and other resources within the data domain service (folders, items, and versions).

- Each relationship is defined by the id of the object at the other end of the relationship, together with type, attributes, and relationships links.
- Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.
- The response body will have an included array that contains the ref resources that are involved in the relationship, which is essentially the response to the [List Custom Relationships for a Version](/en/docs/data/v2/reference/http/projects-project_id-versions-version_id-relationships-refs-GET/) operation. 

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The list of resources was successfully returned.

---

### List Custom Relationships for a Version

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}/relationships/refs`
**Operation ID:** `getVersionRelationshipsRefs`

#### Description
Returns the custom relationships for the specified version. 

Custom relationships can be established between a version of an item and other resources within the data domain service (folders, items, and versions).

- Each relationship is defined by the id of the object at the other end of the relationship, together with type, specific reference meta including extension data.
- Callers will typically use a filter parameter to restrict the response to the custom relationship types (``filter[meta.refType]``) they are interested in.
- The response body will have an included array that contains the resources in the relationship, which is essentially the response to the [List Related Resources operation](/en/docs/data/v2/reference/http/projects-project_id-versions-version_id-relationships-refs-POST/).
- To get custom relationships for multiple versions, see the ListRefs command.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_type_version`
- Ref: `#/components/parameters/filter_id`
- Ref: `#/components/parameters/filter_refType`
- Ref: `#/components/parameters/filter_direction`
- Ref: `#/components/parameters/filter_extension_type`

#### Responses
- **200**: The custom relationships for the version was returned successfully.

---

### Create a Custom Relationship for a Version

**Endpoint:** `POST /data/v1/projects/{project_id}/versions/{version_id}/relationships/refs`
**Operation ID:** `postVersionRelationshipsRef`

#### Description
Creates a custom relationship between a version of an item and another resource within the data domain service (folder, item, or version).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/RelationshipRefsRequest`

#### Responses
- **204**: The custom relationship was successfully created.

---

### List Links for a Version

**Endpoint:** `GET /projects/{project_id}/versions/{version_id}/relationships/links`
**Operation ID:** `getVersionRelationshipsLinks`

#### Description
Returns a collection of links for the specified version of an item. Custom relationships can be established between a version of an item and other external resources residing outside the data domain service. A link’s href defines the target URI to access the resource.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: Successful retrieval of the links collection associated with a specific resource.OK

---

### Create a Storage Location in OSS

**Endpoint:** `POST /data/v1/projects/{project_id}/storage`
**Operation ID:** `postStorage`

#### Description
Creates a placeholder for an item or a version of an item in the OSS. Later, you can upload the binary content for the item or version to this storage location.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/StorageRequest`

#### Responses
- **201**: The storage location was created successfully.

---

### Create a Folder

**Endpoint:** `POST /data/v1/projects/{project_id}/folders`
**Operation ID:** `postFolder`

#### Description
Creates a new folder in the specified project. Use the ``parent`` attribute in the request body to specify where in the hierarchy the new folder should be located. Folders can be nested up to 25 levels deep.

Use the `Modify a Folder </en/docs/data/v2/reference/http/projects-project_id-folders-folder_id-PATCH/>`_ operation to delete and restore folders.

Before you use the Data Management API to access BIM 360 Docs folders, provision your app through the BIM 360 Account Administrator portal. For details, see the [Manage Access to Docs tutorial](/en/docs/bim360/v1/tutorials/getting-started/manage-access-to-docs/).

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/CreateFolder`

#### Responses
- **201**: Successful creation of a folder.

---

### Create an Item

**Endpoint:** `POST /data/v1/projects/{project_id}/items`
**Operation ID:** `postItem`

#### Description
Creates the first version of a file (item). To create additional versions of an item, use POST versions.

Before you create the first version of an item, you must create a placeholder for the file, and upload the file to the placeholder. For more details about the workflow, see the tutorial on uploading a file.

This operation also allows you to create a new item by copying a specific version of an existing item to another folder. The copied version becomes the first version of the new item in the target folder.

**Note:** You cannot copy versions of items across different projects and accounts.

Use the [Create Version](/en/docs/data/v2/reference/http/projects-project_id-versions-POST/) operation with the ``copyFrom`` parameter if you want to create a new version of an item by copying a specific version of another item. 

Before you use the Data Management API to access BIM 360 Docs files, you must provision your app through the BIM 360 Account Administrator portal. For details, see the [Manage Access to Docs tutorial](/en/docs/bim360/v1/tutorials/getting-started/manage-access-to-docs/).

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/copyFrom`
- `x-user-id` in `query` (required: False) — In a two-legged authentication context, the app has access to all users specified by the administrator in the SaaS integrations UI. By providing this header, the API call will be limited to act on behalf of only the user specified.        

Note that for a three-legged OAuth flow or for a two-legged OAuth flow with user impersonation (``x-user-id``), the users of your app must have permission to upload files to the specified parent folder (``data.attributes.relationships.parent.data.id``).

For copying files, users of your app must have permission to view the source folder. 

For information about managing and verifying folder permissions for BIM 360 Docs, see the section on [Managing Folder Permissions](http://help.autodesk.com/view/BIM360D/ENU/?guid=GUID-2643FEEF-B48A-45A1-B354-797DAD628C37).'

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/CreateItem`

#### Responses
- **201**: The first version of an item was successfully created.

---

### Create a Version

**Endpoint:** `POST /data/v1/projects/{project_id}/versions`
**Operation ID:** `postVersion`

#### Description
Creates a new versions of an existing item.

Before creating a new version you must create a storage location for the version in OSS, and upload the file to that location. For more details about the workflow, see the tutorial on uploading a file.

This operation also allows you to create a new version of an item by copying a specific version of an existing item from another folder within the project. The new version becomes the tip version of the item.

Use the [Create an Item](/en/docs/data/v2/reference/http/projects-project_id-items-POST/) operation to copy a specific version of an existing item as a new item in another folder.

This operation can also be used to delete files on BIM360 Document Management. For more information, please refer to the delete and restore a file tutorial.

Before you use the Data Management API to access BIM 360 Docs files, you must provision your app through the BIM 360 Account Administrator portal. For details, see the [Manage Access to Docs tutorial](/en/docs/bim360/v1/tutorials/getting-started/manage-access-to-docs/).

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/copyFrom`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/CreateVersion`

#### Responses
- **201**: Successful creation of a version.
- **409**: Conflict

---

### List Supported Download Formats

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}/downloadFormats`
**Operation ID:** `getVersionDownloadFormats`

#### Description
Returns a list of file formats the specified version of an item can be downloaded as.

**Note:** This operation supports Autodesk Construction Cloud (ACC) Projects. For more information, see the [ACC Platform API documentation](https://en.docs.acc.v1/overview/introduction/).

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The list of file formats that the version can be downloaded as was successfully retrieved.

---

### List Available Download Formats

**Endpoint:** `GET /data/v1/projects/{project_id}/versions/{version_id}/downloads`
**Operation ID:** `getVersionDownloads`

#### Description
Returns the list of file formats of the specified version of an item currently available for download.

**Note:** This operation is not fully implemented as yet. It currently returns an empty data object.

#### Parameters
- Ref: `#/components/parameters/x-user-id`
- Ref: `#/components/parameters/filter_format_fileType`

#### Responses
- **200**: The list of available downloadformats was successfully retrieved.

---

### Get Download Details

**Endpoint:** `GET /data/v1/projects/{project_id}/downloads/{download_id}`
**Operation ID:** `getDownload`

#### Description
Returns the details of a downloadable format of a version of an item.

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: The details of the specified download were retrieved successfully.

---

### Create Download

**Endpoint:** `POST /data/v1/projects/{project_id}/downloads`
**Operation ID:** `postDownload`

#### Description
Kicks off a job to generate the specified download format of the version. Once the job completes, the specified format becomes available for download.

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`
  - Schema: `#/components/schemas/CreateDownload`

#### Responses
- **202**: A job to generate the download format was successfully started.

---

### Check Download Creation Progress

**Endpoint:** `GET /data/v1/projects/{project_id}/jobs/{job_id}`
**Operation ID:** `getDownloadJob`

#### Description
Checks the status of a job that generates a downloadable format of a version of an item. 

**Note**: If the job has finished, this operation returns a HTTP status 303, with the ``location`` return header set to the URI that returns the details of the download.

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Responses
- **200**: Details of the specified job was returned successfully.
- **303**: The request has been redirected to a new location.

---

### Execute a Command

**Endpoint:** `POST /data/v1/projects/{project_id}/commands`
**Operation ID:** `postCommand`

#### Description
Executes the command that you specify in the request body. Commands enable you to perform general operations on multiple resources.

For example, you can check whether a user has permission to delete a collection of versions, items, and folders.

The command as well as the input data for the command are specified using the ``data`` object of the request body. 

For more information about commands see the [Commands](/en/docs/data/v2/overview/commands/) section in the Developer's Guide.

#### Parameters
- Ref: `#/components/parameters/x-user-id`

#### Request Body
- Required: `False`
- Content-Type: `application/vnd.api+json`

#### Responses
- **200**: The command was executed successfully.

---


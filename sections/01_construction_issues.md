## Construction.Issues

_Generated from `Issues.yaml`_

An issue is an item that is created in ACC for tracking, managing and communicating tasks, problems and other points of concern through to resolution. You can manage different types of issues, such as design, safety, and commissioning. We currently support issues that are associated with a project.

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/users/me`
**Operation ID:** `getUserProfile`

#### Description
Returns the current user permissions.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found
- **500**: Internal Server Error

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issue-types`
**Operation ID:** `getIssuesTypes`

#### Description
Retrieves a project’s categories and types.

#### Parameters
- `include` in `query` (required: False) — Use include=subtypes to include the types (subtypes) for each category (type).
- `limit` in `query` (required: False) — Add limit=20 to limit the results count (together with the offset to support pagination).
- `offset` in `query` (required: False) — Add offset=20 to get partial results (together with the limit to support pagination).
- `filter[updatedAt]` in `query` (required: False) — Retrieves types that were last updated at the specified date and time, in in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[isActive]` in `query` (required: False) — Filter types by status e.g. filter[isActive]=true will only return active types. Default value: undefined (meaning both active & inactive issue type categories will return).
- Ref: `#/components/parameters/x-ads-region`

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found
- **500**: Internal Server Error

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issue-attribute-definitions`
**Operation ID:** `getAttributeDefinitions`

#### Description
Retrieves information about issue custom attributes (custom fields) for a project, including the custom attribute title, description and type.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`
- `limit` in `query` (required: False) — The number of custom attribute definitions to return in the response payload. For example, limit=2. Acceptable values: 1-200. Default value: 200.
- `offset` in `query` (required: False) — The number of custom attribute definitions you want to begin retrieving results from.
- `filter[createdAt]` in `query` (required: False) — Retrieves items that were created at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[updatedAt]` in `query` (required: False) — Retrieves items that were last updated at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[deletedAt]` in `query` (required: False) — Retrieves types that were deleted at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[dataType]` in `query` (required: False) — Retrieves issue custom attribute definitions with the specified data type. Possible values: list (this corresponds to dropdown in the UI), text, paragraph, numeric. For example, filter[dataType]=text,numeric.

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found
- **500**: Internal Server Error

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issue-attribute-mappings`
**Operation ID:** `getAttributeMappings`

#### Description
Retrieves information about the issue custom attributes (custom fields) that are assigned to issue categories and issue types.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`
- `limit` in `query` (required: False) — The number of custom attribute mappings to return in the response payload. For example, limit=2. Acceptable values: 1-200. Default value: 200.
- `offset` in `query` (required: False) — The number of custom attribute mappings you want to begin retrieving results from.
- `filter[createdAt]` in `query` (required: False) — Retrieves items that were created at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[updatedAt]` in `query` (required: False) — Retrieves items that were last updated at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[deletedAt]` in `query` (required: False) — Retrieves types that were deleted at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[attributeDefinitionId]` in `query` (required: False) — Retrieves issue custom attribute mappings associated with the specified issue custom attribute definitions. Separate multiple values with commas. For example: filter[attributeDefinitionId]=18ee5858-cbf1-451a-a525-7c6ff8156775.
- `filter[mappedItemId]` in `query` (required: False) — Retrieves issue custom attribute mappings associated with the specified items (project, type, or subtype). Separate multiple values with commas. For example: filter[mappedItemId]=18ee5858-cbf1-451a-a525-7c6ff8156775. Note that this does not retrieve inherited custom attribute mappings or custom attribute mappings of descendants.

#### Responses
- **200**: OK

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issue-root-cause-categories`
**Operation ID:** `getRootCauseCategories`

#### Description
Retrieves a list of supported root cause categories and root causes that you can allocate to an issue. For example, communication and coordination.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`
- `include` in `query` (required: False) — Add ‘include=rootcauses’ to add the root causes for each category.
- `limit` in `query` (required: False) — Add limit=20 to limit the results count (together with the offset to support pagination).
- `offset` in `query` (required: False) — Add offset=20 to get partial results (together with the limit to support pagination)
- `filter[updatedAt]` in `query` (required: False) — Retrieves root cause categories updated at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.

#### Responses
- **200**: OK
- **400**: Bad Request
- **401**: Unauthorized
- **403**: Forbidden
- **404**: Not Found
- **500**: Internal Server Error

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issues`
**Operation ID:** `getIssues`

#### Description
Retrieves information about all the issues in a project, including details about their associated comments and attachments.

#### Parameters
- `filter[id]` in `query` (required: False) — Filter issues by the unique issue ID. Separate multiple values with commas.
- `filter[issueTypeId]` in `query` (required: False) — Filter issues by the unique identifier of the category of the issue. Note that the API name for category is type. Separate multiple values with commas.
- `filter[issueSubtypeId]` in `query` (required: False) — Filter issues by the unique identifier of the type of the issue. Note that the API name for type is subtype. Separate multiple values with commas.
- `filter[status]` in `query` (required: False) — Filter issues by their status. Separate multiple values with commas.
- `filter[linkedDocumentUrn]` in `query` (required: False) — Retrieves pushpin issues associated with the specified files. We support all file types that are compatible with the Files tool. You need to specify the URL-encoded file item IDs.
- Ref: `#/components/parameters/x-ads-region`
- `filter[dueDate]` in `query` (required: False) — Filter issues by due date, in one of the following URL-encoded format: YYYY-MM-DD. Separate multiple values with commas.
- `filter[startDate]` in `query` (required: False) — Filter issues by start date, in one of the following URL-encoded format: YYYY-MM-DD. Separate multiple values with commas.
- `filter[createdAt]` in `query` (required: False) — Filter issues created at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas
- `filter[createdBy]` in `query` (required: False) — Filter issues by the unique identifier of the user who created the issue. Separate multiple values with commas.
- `filter[updatedAt]` in `query` (required: False) — Filter issues updated at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[updatedBy]` in `query` (required: False) — Filter issues by the unique identifier of the user who updated the issue. Separate multiple values with commas.
- `filter[assignedTo]` in `query` (required: False) — Filter issues by the unique Autodesk ID of the User/Company/Role identifier of the current assignee of this issue. Separate multiple values with commas.
- `filter[rootCauseId]` in `query` (required: False) — Filter issues by the unique identifier of the type of root cause for the issue. Separate multiple values with commas.
- `filter[locationId]` in `query` (required: False) — Retrieves issues associated with the specified location but not the location’s sublocations. To also retrieve issues that relate to the locations’s sublocations use the sublocationId filter. Separate multiple values with commas.
- `filter[subLocationId]` in `query` (required: False) — Retrieves issues associated with the specified unique LBS (Location Breakdown Structure) identifier, as well as issues associated with the sub locations of the LBS identifier. Separate multiple values with commas.
- `filter[closedBy]` in `query` (required: False) — Filter issues by the unique identifier of the user who closed the issue. Separate multiple values with commas. For Example: A3RGM375QTZ7.
- `filter[closedAt]` in `query` (required: False) — Filter issues closed at the specified date and time, in one of the following URL-encoded formats: YYYY-MM-DDThh:mm:ss.sz or YYYY-MM-DD. Separate multiple values with commas.
- `filter[search]` in `query` (required: False) — Filter issues using ‘search’ criteria. this will filter both title and issues display ID. For example, use filter[search]=300
- `filter[displayId]` in `query` (required: False) — Filter issues by the chronological user-friendly identifier. Separate multiple values with commas.
- `filter[assignedToType]` in `query` (required: False) — Filter issues by the type of the current assignee of this issue. Separate multiple values with commas. Possible values: Possible values: user, company, role, null. For Example: user.
- `filter[customAttributes]` in `query` (required: False) — Filter issues by the custom attributes. Each custom attribute filter should be defined by it’s uuid. For example: filter[customAttributes][f227d940-ae9b-4722-9297-389f4411f010]=1,2,3. Separate multiple values with commas.
- `filter[valid]` in `query` (required: False) — Only return valid issues (=no empty type/subtype). Default value: undefined (meaning will return both valid & invalid issues).
- `limit` in `query` (required: False) — Return specified number of issues. Acceptable values are 1-100. Default value: 100.
- `offset` in `query` (required: False) — Return issues starting from the specified offset number. Default value: 0.
- `sortBy` in `query` (required: False) — Sort issue comments by specified fields. Separate multiple values with commas. To sort in descending order add a - (minus sign) before the sort criteria
- `fields` in `query` (required: False) — Return only specific fields in issue object. Separate multiple values with commas.

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found

---

### 

**Endpoint:** `POST /construction/issues/v1/projects/{projectId}/issues`
**Operation ID:** `createIssue`

#### Description
Adds an issue to a project.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/IssuePayload`

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **409**: Conflict

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issues/{issueId}`
**Operation ID:** `getIssueDetails`

#### Description
Retrieves detailed information about a single issue. For general information about all the issues in a project.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found

---

### 

**Endpoint:** `PATCH /construction/issues/v1/projects/{projectId}/issues/{issueId}`
**Operation ID:** `patchIssueDetails`

#### Description
Updates an issue.

To verify whether a user can update issues for a specific project, call GET users/me.

To verify which attributes the user can update, call GET issues/:id and check the permittedAttributes and permittedStatuses lists.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/IssuePayload`

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found

---

### Your GET endpoint

**Endpoint:** `GET /construction/issues/v1/projects/{projectId}/issues/{issueId}/comments`
**Operation ID:** `getComments`

#### Description
Get all the comments for a specific issue.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`
- `limit` in `query` (required: False) — Add limit=20 to limit the results count (together with the offset to support pagination).
- `offset` in `query` (required: False) — Add offset=20 to get partial results (together with the limit to support pagination).
- `sortBy` in `query` (required: False) — Sort issue comments by specified fields. Separate multiple values with commas. To sort in descending order add a - (minus sign) before the sort criteria

#### Responses
- **200**: OK
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found
- **500**: Internal Server Error

---

### 

**Endpoint:** `POST /construction/issues/v1/projects/{projectId}/issues/{issueId}/comments`
**Operation ID:** `CreateComments`

#### Description
Creates a new comment under a specific issue.

#### Parameters
- Ref: `#/components/parameters/x-ads-region`

#### Request Body
- Required: `False`
- Content-Type: `application/json`
  - Schema: `#/components/schemas/CommentsPayload`

#### Responses
- **201**: Created
- **400**: Bad Request
- **403**: Forbidden
- **404**: Not Found
- **409**: Conflict
- **500**: Internal Server Error

---


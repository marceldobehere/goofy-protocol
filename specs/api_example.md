

## API

### Section 1

#### GET PUBLIC INFO
Gets Public Info (No Auth Required)

GET `/api/public-info`

**Input**
None

**Result**

200 OK
```json
{
    "public-key": "XYZ",
    "handle": "handle"
}
```


#### POST PUBLIC INFO
Sets Public Info (Signature Auth Required)

GET `/api/public-info`

**Input**
```json
{
    "public-key": "XYZ",
    "handle": "handle"
}
```

**Result**

200 OK, 403 Forbidden, 401 Unauthorized